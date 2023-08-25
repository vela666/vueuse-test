<template>
  <button @click="openFile">Choose file</button>
</template>

<script setup>
import { computed, watch, reactive, ref, onActivated } from 'vue';

import { useFileSystemAccess } from '@vueuse/core';
const {
  isSupported,
  data,
  file,
  fileName,
  fileMIME,
  fileSize,
  fileLastModified,
  create,
  open,
  save,
  saveAs,
  updateData,
} = useFileSystemAccess({
  dataType: 'ArrayBuffer',
  multiple: true,
  types: [
    {
      description: 'Excel',
      accept: {
        'application/vnd.openxmlformats-officedocument.spreadsheetml.sheet': [
          '.xlsx',
        ],
        'application/vnd.ms-excel': ['.xls'],
      },
    },
  ],
  excludeAcceptAllOption: true,
});

const openFile = async () => {
  try {
    await open();
    console.log(file)
  } catch (err) {
    console.log(err);
  }
};

</script>
