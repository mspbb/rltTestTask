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
        v-on:dragstart="drag(block)"
        v-on:click="select(block)"
      >
        {{ block.name }}
        {{ block.count }}
      </div>
    </div>

    <div class="modal" v-if="showModal">
      <div class="modal__closeButton" @click="closeModal">Close</div>
      <div>{{ selectedBlock.name }}</div>
      <div>path - {{ selectedBlock.path }}</div>
      <div>color - {{ selectedBlock.color }}</div>
      <div>count - {{ selectedBlock.count }}</div>
      <div class="modal__removeBlock">
        <button class="modal__removeButton" @click="removeItem()">
          Remove item
        </button>
        <div class="modal__confirm" v-if="removeConfirmed">
          <input type="number" v-model="numberForDelete" />
          <button @click="confirmClose()">cancel</button
          ><button @click="confirmConfirm(selectedBlock)">ok</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted, onUpdated, ref } from "vue";
let targetForDrag = ref(null);

let slotsArr = ref([]);
let itemRefs = ref([]);

let showModal = ref(false);
let removeConfirmed = ref(false);
let numberForDelete = ref(null);

let selectedBlock = ref("");

let itemsArr = ref([]);

const localSave = JSON.parse(localStorage.getItem("itemSetting"));
if (localSave) {
  itemsArr.value = localSave._value;
} else {
  itemsArr.value = [
    { name: "first", path: 0, ref: 0, color: "green", count: 100 },
    { name: "second", path: 1, ref: 1, color: "green", count: 100 },
    { name: "third", path: 7, ref: 2, color: "green", count: 100 },
  ];
}

function setItemRef(el) {
  if (el) {
    itemRefs.value.push(el);
  }
}

onMounted(() => {
  document.querySelectorAll(".inventory__slot").forEach((e) => {
    slotsArr.value.push(e);
  });

  let refCount = 0;
  itemsArr.value.forEach((e) => {
    slotsArr.value[e.path].append(itemRefs.value[refCount]);
    e.ref = itemRefs.value[refCount];
    refCount++;
  });
});

function select(e) {
  selectedBlock = e;
  console.log(selectedBlock.name);
  openModal();
}

function removeItem(e) {
  removeConfirmed.value = true;
}
function confirmClose() {
  removeConfirmed.value = false;
}
function confirmConfirm(e) {
  if (typeof numberForDelete.value == "number") {
    selectedBlock.count = selectedBlock.count - numberForDelete.value;
    removeConfirmed.value = false;
    if (selectedBlock.count <= 0) {
      itemsArr.value = itemsArr.value.filter((T) => T !== e);
    }
  }
  localStorage.setItem("itemSetting", JSON.stringify(itemsArr));
}

function openModal() {
  showModal.value = false;
  if (!showModal.value) {
    showModal.value = true;
  }
}

function closeModal() {
  showModal.value = false;
  removeConfirmed.value = false;
}

function drag(e) {
  targetForDrag = e;
}
function dragDrop(e) {
  e.preventDefault();

  if (e.target.classList.contains("inventory__slot")) {
    let data = targetForDrag.ref;
    e.target.appendChild(data);

    slotsArr.value.forEach((el) => {
      if (el == e.target) {
        targetForDrag.path = slotsArr.value.indexOf(el);
      }
    });
    localStorage.setItem("itemSetting", JSON.stringify(itemsArr));
  } else {
    let needsBlocks = e.composedPath();
    needsBlocks.forEach((e) => {
      if (e.className == "inventory__slot") {
        let data = targetForDrag.ref;

        e.appendChild(data);

        slotsArr.value.forEach((el) => {
          if (el == e.target) {
            targetForDrag.path = slotsArr.value.indexOf(el);
          }
        });
        localStorage.setItem("itemSetting", JSON.stringify(itemsArr));
      }
    });
  }
}
function allowDrop(e) {
  e.preventDefault();
}
</script>

<style src="./style.scss"></style>
