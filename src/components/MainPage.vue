<template>
  <div class="wrapper">
    <div class="preview">
      <h3 class="select-header">Выбор объекта</h3>
      <select  v-model="selectedObject" style="padding: 5px; cursor: pointer;" class="object-select" name="object" id="object">
        <option value="" selected disabled>Выберите имя объекта</option>
        <option v-for="object in objects" :key="object.name" :value="object.name">{{ object.name }}</option>
      </select>
      <div>
        <h3 class="preview-header">Просмотр</h3>
        <div class="preview-name">Имя: {{ selectedObject }}</div>
        <div class="preview-value">Значение: {{ selectedValue }}</div>
      </div>
      <div class="change">
        <h3 style="margin-bottom: 5px">Изменение значения</h3>
        <input @keydown.enter="changeValue" v-model="newValue" style="padding: 4px; margin-bottom: 5px;" type="text" placeholder="Введите новое значение..">
        <button @click="changeValue" style="padding: 4px; cursor: pointer;">Изменить</button>
      </div>
    </div>

  </div>
</template>

<script>
export default {
  data() {
    return {
      objects: require('../data/objects.json'),
      selectedObject: '',
      selectedValue: '',
      newValue: ''
    }
  },
  methods: {
    changeValue() {
      let target = this.objects.findIndex(object => object.name === this.selectedObject)
      if (this.newValue !== '') {
        this.objects[target].value = this.newValue
        this.setValue()
        this.newValue = ''
      }
    },
    setValue() {
      this.selectedValue = this.objects.find(object => object.name === this.selectedObject).value
    }
  },
  watch: {
    selectedObject() {
      this.setValue()
    }
  }
}
</script>


<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  background-color: #96cdf5;
}
.wrapper {
  display: flex;
  justify-content: space-around;
  align-self: center;
}
.preview {
  display: flex;
  flex-direction: column;
  border: 1px solid black;
  width: 400px;
  height: 400px;
  background-color: #80B8FA;
  padding: 80px;
}
.change {
  display: flex;
  flex-direction: column;
  background-color: #80B8FA;
}
.select-header {
  margin-bottom: 5px;
}
.preview-header {
  margin-bottom: 10px;
}
.preview-name {
  margin-bottom: 5px;
}
.preview-value {
  margin-bottom: 20px;
}
.object-select {
  margin-bottom: 20px;
}
</style>
