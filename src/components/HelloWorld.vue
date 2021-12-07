<template>
  <div class="hello">
    <div class="container">
      <label>Key 1: </label>
      <input v-model="key1" @input="createSquareOne"/>
      <br />
      <label>Key 2: </label>
      <input v-model="key2" @input="createSquareTwo" />
      <br />
      <label>Input message: </label>
      <input v-model="inputMessage"/>
      <br />
      <button @click="encryptString">Encrypt</button>
      <input v-model="encryptedMessage" />
      <br />
      <button @click="decryptString">Decrypt</button>
      <input v-model="decryptedMessage"/>
      <br />
      <br />

      <div class="container">
        <div class="row">
          <div class="col">
            <div v-for="row in regSquare" :key="row">
              <span v-for="letter in row" :key="letter">
                {{letter}} &nbsp;
              </span>
            </div>
          </div>
        


          <div class="col">
            <div v-for="row in squareOne" :key="row">
              <span v-for="(letter) in row" :key="letter">
                {{letter}} &nbsp;
              </span>
            </div>
          </div>
        </div>



        <div class="row">
          <div class="col">
            <div v-for="row in squareTwo" :key="row">
              <span v-for="letter in row" :key="letter">
                {{letter}} &nbsp;
              </span>
            </div>
          </div>
    
          <div class=col>
            <div v-for="row in regSquare" :key="row">
              <span v-for="letter in row" :key="letter">
                  {{letter}} &nbsp;
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
  name: 'HelloWorld',
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
      var keyArray = this.key1.toLowerCase().replace(/j/g,'i').split('');
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
      var keyArray = this.key2.toLowerCase().replace(/j/g,'i').split('');
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
      var messageInput = this.inputMessage.toLowerCase().replace(/j/g,'i').split('');
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
      var messageInput = this.inputMessage.toLowerCase().replace(/j/g,'i').split('');
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
      this.decryptedMessage = messageOutput
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

    // makeRows() {
    //   let squares = [this.regSquare, this.squareOne, this.regSquare, this.squareTwo];
    //   let row = [];
    //   let i, l, chunkSize = this.rowSize;

    //   for(i = 0, l = squares.length; i < l; i += chunkSize) {
    //     row.push(squares.slice(i, i+chunkSize))
    //   }
    //   return row;    
    // }

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.col {
  border-style: solid;
}
.row {
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
