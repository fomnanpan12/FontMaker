<script setup>
import { ref, computed, reactive, onMounted } from 'vue';
import html2canvas from 'html2canvas'; // Import the html2canvas library

const textInput = ref('');
const fontSize = ref(20);
const newFontFamily = ref('cursive');
const newColor = ref('#000000');
const newBackgroundColor = ref('#8FBC8F')

let newFontSize = computed(() => {
  return fontSize.value + 'px';
});

const newStyle = reactive({
  fontSize: newFontSize,
  fontFamily: newFontFamily,
  color: newColor,

});

const checkWidth = computed(() => {
    if(newFontSize == 100 && textInput.value.length > 13) {
        return fit-content
    }
})

const newPreviewBox = reactive({
    backgroundColor: newBackgroundColor, 
    width: checkWidth,
})


// Function to download the result as a PNG
const downloadAsPNG = () => {
  const resultElement = document.querySelector('.result');

  if (resultElement) {
    html2canvas(resultElement).then((canvas) => {
      const link = document.createElement('a');
      link.href = canvas.toDataURL('image/png');
      link.download = 'result.png';
      link.click();
    });
  }
};

// Check if the text input is too long (more than 50 characters)
const checklength = 20;

</script>

<template>
  <div class="fontStyle">
    <div class="iChild">
      <label>Enter Text:</label>
      <input type="text" v-model="textInput" :maxlength="[checklength]"  id="name">
    </div>
    <div class="iChild">
      <label>Choose a font-family:</label>
      
      <select name="cars" v-model="newFontFamily" id="fFamily">
        <option value="cursive">Cursive</option>
        <option value="Times New Roman">Times New Roman</option>
        <option value="sans-serif">Sans-serif</option>
        <option value="courier">Courier</option>
        
        <!-- <option value="'fantasy', Papyrus">Fantasy Papyrus</option>
        <option value="'cursive', Brush Script MT">Cursive Brush Script MT</option> -->


        
      </select>
    </div>
    <div class="iChild">
        <label>Choose Color: </label>
        <input type="color" v-model="newColor" name="" id="">
    </div>
    <div class="iChild">
      <label>Adjust Size {{ newFontSize }}</label> <br>

      <input type="range" v-model="fontSize" id="fontSizeRange">
    </div>
    <div class="iChild">
        <label>Background color: </label>
        <input type="color" v-model="newBackgroundColor" name="" id="">
    </div>


  </div>
 
  <div class="get">
    <h2>Preview</h2>
    <div class="result" :style="[newPreviewBox]">
      <h1 :style="[newStyle]"> {{ textInput }}</h1>
    </div>
  </div>
  <div class="getFont">
    <button id="download" @click="downloadAsPNG">DOWNLOAD</button>
  </div>
</template>

<style>
.fontStyle {
  display: grid;
  width: 40rem;
  padding: 1rem;
  font-size: 1.3rem;
  border: 3px solid rgb(1, 255, 86);
}

.iChild {
  margin: 1rem;
  font-family: sans-serif
}

#name {
  height: 1.5rem;
  border: 1px black solid;
  border-radius: 8px;
}

#fontSizeRange {
  width: 60%; /* Ensure the range input spans the entire width */
}

.result {
  border: 3px solid rgb(21, 255, 0);
  margin-top: 1rem;
  padding: 1rem;

  /* max-width: 50vw; */

}

.getFont{
    margin-top: 3rem;
}

#download{
    padding: 1rem;
    width: 15rem;
    font-size: 1.5rem;
    background-color: rgb(0, 255, 0);
    color: white;
}
</style>
ChatGPT