<script setup lang="ts">
const emit = defineEmits(["close"]);

defineProps({
  alertColor: String,
  place: String,
  title: String,
  magnitude: Number,
  link: String,
  showDialog: Boolean,
});

const closeDialog = () => {
  emit("close");
};

document.getElementById("overlay")?.addEventListener("click", function () {
  closeDialog();
});

document.getElementById("dialog")?.addEventListener("click", function (event) {
  event.stopPropagation();
});
</script>

<template>
  <div
    v-if="showDialog"
    class="dialog-overlay"
    id="overlay"
    @click="closeDialog"
  >
    <div
      id="dialog"
      class="dialog"
      @click.stop
    >
      <div class="dialog-header">
        <h2>{{ title }}</h2>
        <button
          class="close-button"
          @click="closeDialog"
        >
          &times;
        </button>
      </div>
      <div
        class="colorful-patch"
        :style="{ backgroundColor: alertColor }"
      />
      <p>Place: {{ place }}</p>
      <p>Magnitude: {{ magnitude }}</p>
      <a
        :href="link"
        class="info-link"
        target="_blank"
        rel="noopener noreferrer"
      >
        More info
      </a>
    </div>
  </div>
</template>

<style scoped>
.dialog-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: start;
  padding-top: 5rem;
  z-index: 1000;
}

.dialog {
  background-color: black;
  border-radius: 5px;
  padding: 20px;
  width: 1000px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.dialog-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.close-button {
  border: none;
  background-color: white;
  cursor: pointer;
  font-size: 1.5rem;
}

.colorful-patch {
  width: 100px;
  height: 100px;
}

p {
  margin: 10px 0;
}
</style>
