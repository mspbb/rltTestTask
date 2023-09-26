<template>
  <div class="inventory__wrapper">
    <div class="inventory__slot" v-on:drop="dragDrop" v-on:dragover="allowDrop">
      <div class="inventory__item" draggable="true" v-on:dragstart="drag"></div>
    </div>
    <div
      class="inventory__slot"
      v-on:drop="dragDrop"
      v-on:dragover="allowDrop"
    ></div>
    <div class="inventory__slot" v-on:drop="dragDrop" v-on:dragover="allowDrop">
      <div
        class="inventory__item"
        draggable="true"
        v-on:dragstart="drag"
        v-on:click="click"
      ></div>
    </div>
    <div
      class="inventory__slot"
      v-on:drop="dragDrop"
      v-on:dragover="allowDrop"
    ></div>
    <div
      class="inventory__slot"
      v-on:drop="dragDrop"
      v-on:dragover="allowDrop"
    ></div>

    <div
      class="inventory__slot"
      v-on:drop="dragDrop"
      v-on:dragover="allowDrop"
    ></div>
    <div
      class="inventory__slot"
      v-on:drop="dragDrop"
      v-on:dragover="allowDrop"
    ></div>
    <div
      class="inventory__slot"
      v-on:drop="dragDrop"
      v-on:dragover="allowDrop"
    ></div>
    <div
      class="inventory__slot"
      v-on:drop="dragDrop"
      v-on:dragover="allowDrop"
    ></div>
    <div
      class="inventory__slot"
      v-on:drop="dragDrop"
      v-on:dragover="allowDrop"
    ></div>

    <div
      class="inventory__slot"
      v-on:drop="dragDrop"
      v-on:dragover="allowDrop"
    ></div>
    <div
      class="inventory__slot"
      v-on:drop="dragDrop"
      v-on:dragover="allowDrop"
    ></div>
    <div
      class="inventory__slot"
      v-on:drop="dragDrop"
      v-on:dragover="allowDrop"
    ></div>
    <div
      class="inventory__slot"
      v-on:drop="dragDrop"
      v-on:dragover="allowDrop"
    ></div>
    <div
      class="inventory__slot"
      v-on:drop="dragDrop"
      v-on:dragover="allowDrop"
    ></div>

    <div
      class="inventory__slot"
      v-on:drop="dragDrop"
      v-on:dragover="allowDrop"
    ></div>
    <div
      class="inventory__slot"
      v-on:drop="dragDrop"
      v-on:dragover="allowDrop"
    ></div>
    <div
      class="inventory__slot"
      v-on:drop="dragDrop"
      v-on:dragover="allowDrop"
    ></div>
    <div
      class="inventory__slot"
      v-on:drop="dragDrop"
      v-on:dragover="allowDrop"
    ></div>
    <div
      class="inventory__slot"
      v-on:drop="dragDrop"
      v-on:dragover="allowDrop"
    ></div>

    <div
      class="inventory__slot"
      v-on:drop="dragDrop"
      v-on:dragover="allowDrop"
    ></div>
    <div
      class="inventory__slot"
      v-on:drop="dragDrop"
      v-on:dragover="allowDrop"
    ></div>
    <div
      class="inventory__slot"
      v-on:drop="dragDrop"
      v-on:dragover="allowDrop"
    ></div>
    <div
      class="inventory__slot"
      v-on:drop="dragDrop"
      v-on:dragover="allowDrop"
    ></div>
    <div
      class="inventory__slot"
      v-on:drop="dragDrop"
      v-on:dragover="allowDrop"
    ></div>

    <div class="modal" v-if="showModal">some text</div>
  </div>
</template>

<script setup>
import { ref } from "vue";

let targetForDrag = ref(null);
let showModal = ref(false);

function click(e) {
  if (!showModal.value) {
    showModal.value = true;
  } else {
    showModal.value = false;
  }
}

function drag(e) {
  targetForDrag = e.target;
}
function dragDrop(e) {
  e.preventDefault();

  if (e.target.classList.contains("inventory__slot")) {
    var data = targetForDrag;
    e.target.appendChild(data);
  } else {
    let needsBlocks = e.composedPath();
    needsBlocks.forEach((e) => {
      if (e.className == "inventory__slot") {
        var data = targetForDrag;
        e.appendChild(data);
      }
    });
  }
}
function allowDrop(e) {
  e.preventDefault();
}
</script>

<style src="./style.scss"></style>
