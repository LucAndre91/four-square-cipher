<template>
  <div class="hello">
    <div class="container">
      <h1 class="title">Four Square Cipher</h1>
      <div class="form">
        <label>Key 1 (for upper-right square): </label>
        <input v-model="key1" @input="createSquareOne"/>
        <br />
        <label>Key 2 (for lower-left square): </label>
        <input v-model="key2" @input="createSquareTwo" />
        <br />
        <label>Input message: </label>
        <input v-model="inputMessage"/>
        <br />
        <div class="buttons">
          <button @click="encryptString">Encrypt</button>
          <button @click="decryptString">Decrypt</button>
        </div>
        <label>Output message:</label>
        <input v-model="encryptedMessage" />
        <br />
      
        <br />
        <br />
      </div>

      <div class="squares">
        <div class="row">
          <div class="col">
            <div class="squareRow" v-for="row in regSquare" :key="row">
              <span class="grid" v-for="letter in row" :key="letter">
                {{letter}} 
              </span>
            </div>
          </div>
        


          <div class="col">
            <div class="squareRow" v-for="row in squareOne" :key="row">
              <span class="grid" v-for="(letter) in row" :key="letter">
                {{letter}}
              </span>
            </div>
          </div>
        </div>



        <div class="row">
          <div class="col">
            <div class="squareRow" v-for="row in squareTwo" :key="row">
              <span class="grid" v-for="letter in row" :key="letter">
                {{letter}} 
              </span>
            </div>
          </div>
    
          <div class="col">
            <div class="squareRow" v-for="row in regSquare" :key="row">
              <span class="grid" v-for="letter in row" :key="letter">
                  {{letter}} 
              </span>
            </div>
          </div>
    
        </div>
      </div>

    </div>
  </div>
</template>

<script>
export default {
  name: 'Cipher',
  props: {
    msg: String
  },
  data() {
    return {
      key1: '',
      key2:'',
      alphabet: 'abcdefghiklmnopqrstuvwxyz'.split(''),
      squareOneLetters: 'abcdefghiklmnopqrstuvwxyz'.split(''),
      squareTwoLetters: 'abcdefghiklmnopqrstuvwxyz'.split(''),
      firstSquare: 'abcdefghiklmnopqrstuvwxyz'.split(''),
      secondSquare: 'abcdefghiklmnopqrstuvwxyz'.split(''),
      inputMessage: '',
      encryptedMessage: '',
      decryptedMessage: ''
    }
  },
  methods: {
    createSquareOne() {
      var keyArray = this.key1.toLowerCase().replace(/j/g,'i').replace(/[^a-zA-Z]/g, '').split('');
      let keyWord = [];
      let alphabet = 'abcdefghiklmnopqrstuvwxyz'.split('');

      for(let i = 0; i < keyArray.length; i++) {
        if(!keyWord.includes(keyArray[i])) {
          keyWord.push(keyArray[i])
        }
      }

      for(let i = 0; i < keyWord.length; i++) {
        if(this.alphabet.includes(keyWord[i])) {
          let index = alphabet.indexOf(keyWord[i])
          alphabet.splice(index, 1)
        }
      }
      this.squareOneLetters = keyWord.concat(alphabet);
    },
    createSquareTwo() {
      var keyArray = this.key2.toLowerCase().replace(/j/g,'i').replace(/[^a-zA-Z]/g, '').split('');
      let keyWord = [];
      let alphabet = 'abcdefghiklmnopqrstuvwxyz'.split('');
      for(let i = 0; i < keyArray.length; i++) {
        if(!keyWord.includes(keyArray[i])) {
          keyWord.push(keyArray[i])
        }
      }
      for(let i = 0; i < keyWord.length; i++) {
        if(alphabet.includes(keyWord[i])) {
          let index = alphabet.indexOf(keyWord[i])
          alphabet.splice(index, 1)
        }
      }
      this.squareTwoLetters = keyWord.concat(alphabet)
    },
    encryptString() {
      var square1 = this.squareOneLetters;
      var square2 = this.squareTwoLetters;
      var alphabet = this.alphabet;
      var messageOutput = "";
      var messageInput = this.inputMessage.toLowerCase().replace(/j/g,'i').replace(/[^a-zA-Z]/g, '').split('');
      var pos = 0;

      while(pos < messageInput.length) {
        var m1 =  messageInput[pos];
        var m2 = '';
        
        if(pos + 1 < messageInput.length) {
          m2 = messageInput[pos + 1];
          pos += 2;
        } else {
          m2 = 'q' //dummy letter
          pos += 1;
        }
      var index1 = alphabet.indexOf(m1);
      var index2 = alphabet.indexOf(m2);
      var c1 = square1[(5 * Math.floor(index1 / 5)) + index2 % 5]
      var c2 = square2[(5 * Math.floor(index2 / 5)) + index1 % 5] 

       messageOutput = messageOutput.concat(c1);
       messageOutput = messageOutput.concat(c2);

      }
        this.encryptedMessage = messageOutput
        return messageOutput
      
    },
    decryptString() {
      var square1 = this.squareOneLetters;
      var square2 = this.squareTwoLetters;
      var alphabet = this.alphabet;
      var messageOutput = "";
      var messageInput = this.inputMessage.toLowerCase().replace(/j/g,'i').replace(/[^a-zA-Z]/g, '').split('');
      var pos = 0;

      while(pos < messageInput.length) {
        var m1 =  messageInput[pos];
        var m2 = '';
        
        if(pos + 1 < messageInput.length) {
          m2 = messageInput[pos + 1];
          pos += 2;
        } else {
          m2 = 'q' //dummy letter
          pos += 1;
        }
        var index1 = square1.indexOf(m1);
        var index2 = square2.indexOf(m2);
        var c1 = alphabet[(5 * Math.floor(index1 / 5)) + index2 % 5]
        var c2 = alphabet[(5 * Math.floor(index2 / 5)) + index1 % 5]
        messageOutput = messageOutput.concat(c1);
        messageOutput = messageOutput.concat(c2);
      }
      this.encryptedMessage = messageOutput
      return messageOutput
    }
  },
  computed: {
    squareOne() {
      var arr = [];
      var A = this.squareOneLetters;
      var rows = Math.sqrt(A.length);
      for(var i = 0; i < rows; i++) {
        arr[i] = [];
        for(var j = 0; j < rows; j++) {
          arr[i][j] = A[i * rows + j];
        }
      }
      
      return arr;

    },
    squareTwo() {
      var arr = [];
      var A = this.squareTwoLetters;
      var rows = Math.sqrt(A.length);
      for(var i = 0; i < rows; i++) {
        arr[i] = [];
        for(var j = 0; j < rows; j++) {
          arr[i][j] = A[i * rows + j];
        }
      }
      return arr;
    },
    regSquare() {
      var arr = [];
      var A = this.alphabet;
      var rows = Math.sqrt(A.length);
      for(var i = 0; i < rows; i++) {
        arr[i] = [];
        for(var j = 0; j < rows; j++) {
          arr[i][j] = A[i * rows + j];
        }
      }
      return arr;
    },

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.title {
  font-family: 'Lucida Console', Courier, monospace;
  margin-bottom: 50px;
}
.form {
  margin: auto;
  width: 500px;
  text-align: left;
  clear: both;

}
.form input {
  width: 100%;
  height: 20px;
  border-radius: 8px;
  clear: both;
  margin-top: 3px;
  margin-bottom: 5px;
}
.form input:focus {
  outline: none;
}
.buttons button {
  height: 30px;
  border-radius: 5px;
  margin-right: 10px;
  margin-top: 10px;
  margin-bottom: 10px;
  font-weight: bold;
  cursor: pointer;
}
.col {
  width: 12%;
  margin: 5px;
  border: 1px solid black;
}
.row {
  display: flex;
  align-items: center;
  justify-content: center;
}
.grid {
  border: 1px solid black;
  width: 100%;
}
.squareRow {
  display: flex;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
