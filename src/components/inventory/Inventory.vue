<template>
  <div class="inventory__wrapper">
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
    <div class="inventory__slot" v-on:drop="dragDrop" v-on:dragover="allowDrop">
      <div
        class="inventory__item"
        v-for="block in itemsArr"
        :key="block.name"
        :ref="setItemRef"
        draggable="true"
        v-on:dragstart="drag"
        v-on:click="click"
      >
        {{ block.name }}
      </div>
    </div>

    <div class="modal" v-if="showModal">some text</div>
  </div>
</template>

<script setup>
import { onMounted, onUpdated, ref } from "vue";
const squareExample = ref(null);

let targetForDrag = ref(null);
let showModal = ref(false);
let slotsArr = ref([]);
let itemRefs = ref([]);

function setItemRef(el) {
  if (el) {
    itemRefs.value.push(el);
  }
}

let itemsArr = ref([
  { name: "first", path: 0, ref: 0 },
  { name: "second", path: 1, ref: 1 },
  { name: "third", path: 7, ref: 2 },
]);

onMounted(() => {
  document.querySelectorAll(".inventory__slot").forEach((e) => {
    slotsArr.value.push(e);
  });

  itemsArr.value.forEach((e) => {
    slotsArr.value[e.path].append(itemRefs.value[e.ref]);
    e.ref = itemRefs.value[e.ref];
  });
});

function click(e) {
  if (!showModal.value) {
    showModal.value = true;
    console.log(e.target);
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
