<template>
  <div class="main-box">
    <div class="app">
      <h1>{{ title }}</h1>
      <div class="box">
        <div class="form">
          <div class="form-group">
            <div class="form-group">
              <label>Note title</label>
              <input type="text" v-model="note.title" />
            </div>
            <div class="form-group">
              <label>Note text</label>
              <textarea type="text" v-model="note.text" rows="3"></textarea>
            </div>
            <button class="btn" @click="addNote" v-if="note.text && note.title">
              Add note
            </button>
          </div>
        </div>
        <div class="put-notes" v-if="notes.length != 0">
          <div class="note-container">
            <div class="note" v-for="(note, index) in notes" :key="index">
              <button class="close-btn" @click="removeNote(index)">X</button>
              <p class="note-paragraph">{{ note.title }}{{ index }}</p>
              <p class="note-paragraph">{{ note.date }}</p>
              <p class="note-paragraph">{{ note.text }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: "Sticky Note",
      note: {
        title: "",
        text: "",
      },
      notes: [],
    };
  },
  methods: {
    addNote() {
      let { text, title } = this.note;
      this.notes.push({
        text,
        title,
        date: new Date(Date.now()).toLocaleString(),
      });
      this.note.text = "";
      this.note.title = "";
    },
    removeNote(index) {
      this.notes.splice(index, 1);
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
h1 {
  margin-bottom: 30px;
}
.app {
  padding: 15px;
  text-align: center;
  margin: 0 auto;
}

label {
  display: block;
  margin: 0 auto;
}

input {
  max-width: 180px;
}

textarea {
  max-width: 180px;
}

.box {
  display: flex;
  justify-content: space-between;
}

.form {
  flex-grow: 1;
}

.btn {
  background-color: rgb(79, 131, 243);
  padding: 10px;
  cursor: pointer;
}

.btn:hover {
  transform: scale(1.05);
  box-shadow: 0 0 4px black;
  transition: 0.2s;
}

.put-notes {
  flex-grow: 3;
  min-width: 50vw;
  margin: 0 auto;
}
.note-container {
  display: flex;
  flex-wrap: wrap;
  /* max-width: 50vw; */
  justify-content: center;
}
.note {
  background-color: rgb(247, 245, 157);
  color: black;
  padding: 10px;
  padding-top: 20px;
  box-shadow: 0 0 2px 0 black;
  min-width: 150px;
  min-height: 150px;
  margin: 10px;
  position: relative;
}
.close-btn {
  position: absolute;
  top: 0;
  right: 0;
  background: rgb(79, 131, 243);
  color: white;
  width: 20px;
  height: 20px;
  line-height: 20px;
  font-size: 20px;
  cursor: pointer;
  border-radius: 0;
  z-index: 1;
  padding: 5px !important;
  display: flex;
  justify-content: center;
  align-items: center;
}
p {
  width: 100%;
}
</style>
