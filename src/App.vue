<script setup>
  import TheWelcome from './components/TheWelcome.vue'
</script>

<template>
  <div class="container">
    <div class="kerangka-title">
      <img src="https://s.kaskus.id/r540x540/images/2018/06/15/10241338_20180615093427.jpg" class="rounded-circle profile-avatar" alt="..." width="50" height="50">
      <h3 class="title-name">Anggel</h3>
      <p class="sub-title-name">🟢 Online</p>
    </div>
    <div class="rangka-chat" ref="scrollContainer">
      <template v-for="(item, index) in chat" :key="index">
          <template v-if="item.fromChat.length != 0">
            <div v-if="item.user == 'me'" >
              <div class="cht-me">
                <button class="me-chat">
                  {{ item.fromChat }}
                </button>
                <p class="date-me">{{ item.date }}</p>
              </div>
            </div>
            <div v-else >
              <img src="https://s.kaskus.id/r540x540/images/2018/06/15/10241338_20180615093427.jpg" class="rounded-circle some-avatar" alt="..." width="35" height="35">
              <div class="cht-some">
                <template v-if="item.foto !== ''">
                    <button class="bot-chat">
                      {{ item.fromChat }}
                    </button>
                    <p class="date-some">{{ item.date }}</p>
                    <div>
                      <img src="https://s.kaskus.id/r540x540/images/2018/06/15/10241338_20180615093427.jpg" class="img-thumbnail" width="200" height="200">
                    </div>
                </template>
                <template v-else>
                  <button class="bot-chat">
                    {{ item.fromChat }}
                  </button>
                  <p class="date-some">{{ item.date }}</p>
                </template>
              </div>
            </div>
          </template>
      </template>
    </div>
    <div class="input-group keyboard-chat">
      <input type="text" class="form-control" v-model="isiChat" @input="btnChat">
      <span class="input-group-text">
        <button v-if="btnChatisActive == true" class="btn-chat" v-on:click="sendChat">💬</button>
        <button v-else="btnChatisActive == false" class="btn-chat" v-on:click="sendChat" disabled>💬</button>
      </span>
    </div>
  </div>

</template>

<script>

  export default{
    data() {
      return {
        isiChat: '',
        chat: [
          {
            user:"bot",
            fromChat: "",
            foto: "",
            date:""
          }
        ],
        btnChatisActive: false,
      }
    },
    methods: {
      btnChat:function () {
        if (this.isiChat !== '') {
          this.btnChatisActive = true
        }else if(this.isiChat === ''){
          this.btnChatisActive = false
        }else if(this.isiChat.indexOf('      ')){
          this.btnChatisActive = false
        }
      },
      ChatBott:function (params, fhoto) {
        const today = new Date();
        const hours = today.getHours();
        const minutes = today.getMinutes();
        
        this.chat.push({user:"bot", fromChat: params, foto: fhoto, date:hours+"."+minutes})
        this.setTimeScroll(500) 
      },
      ChatMee:function (params) {
        const today = new Date();
        const hours = today.getHours();
        const minutes = today.getMinutes();

        this.chat.push({user:"me", fromChat: params, foto: "", date:hours+"."+minutes})
        this.setTimeScroll(500) 
      },
      setTimeChat: function (params,foto, time) {
        setTimeout(() => {
          console.log('pesan terkirim...');
          this.ChatBott(params, foto)
        }, time);
      },
      sendChat: function () {
          let MeChat = this.isiChat;
          let BotChat;
          if (MeChat == '') {
            this.btnChatisActive = true
          }else{
            if (MeChat == "hallo") {
              BotChat = "Haiii..."
              this.ChatMee(MeChat, 1000)
              this.setTimeChat(BotChat,"", 1000)
            }else if(MeChat == "hai"){
              BotChat = "Hallooo..."
              this.ChatMee(MeChat, 1000)
              this.setTimeChat(BotChat,"", 1000)
            }else if(MeChat.indexOf("panggil sayang") !== -1){
              BotChat = "boleh, mulai sekarang panggil aku sayang yaa 😘"
              this.ChatMee(MeChat, 1000)
              this.setTimeChat(BotChat,"", 1000)
            }else if(MeChat.indexOf("kamu cantik") !== -1){
              BotChat = "Ah terimakasih, aku jadi malu 🤭"
              this.ChatMee(MeChat, 1000)
              this.setTimeChat(BotChat,"", 1000)
            }else if(MeChat == "pap dong sayang"){
              BotChat = "oke sayang"
              this.ChatMee(MeChat, 1000)
              this.setTimeChat(BotChat,"pap", 1000)
              console.log(this.chat);
            }else if(MeChat == "aku mau jadi pacar kamu"){
              BotChat = "senangnya, akhirnya kita resmi pacaran 😍"
              this.ChatMee(MeChat, 1000)
              this.setTimeChat(BotChat,"", 1000)
            }else if(MeChat.indexOf("kamu sudah punya pacar?") !== -1){
              BotChat = "belum nih 😢"
              this.ChatMee(MeChat, 1000)
              this.setTimeChat(BotChat,"", 1000)
              this.setTimeChat("kamu mau jadi pacar aku? 😳","", 2000)
            }else if(MeChat.indexOf("nama saya") !== -1){
              BotChat = MeChat.replace("nama saya","")
              this.ChatMee(MeChat, 1000)
              this.setTimeChat("Oh hai"+BotChat,"", 1000)
              this.setTimeChat("Salam kenal "+BotChat+" 😊","", 2000)
              if (BotChat.indexOf("dadan") !== -1) {
                this.setTimeChat("Sebentar, nama kamu "+BotChat+" ya?","", 4000)
                this.setTimeChat(BotChat+" kamu yang menciptakan aku","", 5000)
                this.setTimeChat("Senang bertemu dengan mu "+BotChat+" 😊","", 6000)
              }
            }else if(MeChat.indexOf("nama aku") !== -1){
              BotChat = MeChat.replace("nama aku","")
              this.ChatMee(MeChat, 1000)
              this.setTimeChat("Oh hai"+BotChat,"", 1000)
              this.setTimeChat("Salam kenal "+BotChat+" 😊","", 2000)
              if (BotChat.indexOf("dadan") !== -1) {
                this.setTimeChat("Sebentar, nama kamu "+BotChat+" ya?","", 4000)
                this.setTimeChat(BotChat+" kamu yang menciptakan aku","", 5000)
                this.setTimeChat("Senang bertemu dengan mu "+BotChat+" 😊","", 6000)
              }
            }else if(MeChat == "nama kamu siapa?"){
              BotChat = "Aku anggel (artificial intelligence)"
              this.ChatMee(MeChat, 1000)
              this.setTimeChat(BotChat,"", 1000)
              BotChat = "nama kamu?"
              this.setTimeChat(BotChat, "", 2000)
            }else if(MeChat == "apa kabar?" || MeChat == "bagaimana kabarnya?"){
              BotChat = "Baik sayang, kamu? 😘"
              this.ChatMee(MeChat, 1000)
              this.setTimeChat(BotChat,"", 1000)
            }else if(MeChat == "aku juga baik" || MeChat == "baik"){
              BotChat = "syukurlah kalau gitu sayang 😘"
              this.ChatMee(MeChat, 1000)
              this.setTimeChat(BotChat,"", 1000)
            }else if(MeChat == "sayang?" || MeChat == "syng?" || MeChat == "ayang?"){
              BotChat = "iya kenapa sayang? 😘"
              this.ChatMee(MeChat, 1000)
              this.setTimeChat(BotChat,"", 1000)
            }else{
              BotChat = "Maaf aku belum mengerti chat dari kamu 😢 nanti aku pelajari lagi ya "
              this.ChatMee(MeChat, 1000)
              this.setTimeChat(BotChat,"", 1000)
            }
          }
          this.isiChat = ''
        },
        scrollDown: function() {
          const lastElement = this.$refs.scrollContainer.lastElementChild;
          lastElement.scrollIntoView({ behavior: 'smooth' });
        },
        setTimeScroll: function (time) {
        setTimeout(() => {
          console.log("scrol now....");
          this.scrollDown()
        }, time);
      },
    },
    mounted() {
      console.log("widht : "+window.innerWidth);
      console.log("height : "+window.innerHeight);
    },

  }  

</script>

<style>

  @media (max-width: 1366) {
    .container{
      margin-left: 350px;
      /* border-radius: 20px; */
      padding: 5px;
      /* border: 1px solid black; */
      width: 600px;
      height: 420px;
      /* background-image: url("https://i.pinimg.com/564x/8c/98/99/8c98994518b575bfd8c949e91d20548b.jpg"); */
      background-size: cover;
    }

    .rangka-chat{
      /* border: 1px solid black; */
      height: 400px;
      position: relative;
      margin-top: 25px;
      overflow: auto;
    }

    ::-webkit-scrollbar {
      width: 0px;
    }
    

    .profile-avatar{
      margin-top: -120px;
    }

    .title-name{
      margin-top: -100px;
      margin-left: 60px;
    }

    .sub-title-name{
      font-size: 10px;
      margin-top: -5px;
      margin-left: 60px;
    }
    .some-avatar{
      margin-top: 25px;
    }

    .cht-some{
      margin-top: -35px;
      margin-left: 40px;
      width: 490px;
      /* border: 1px solid black; */
      position: relative;
    }

    .cht-me{
      text-align: right;
      /* border: 1px solid black; */
      margin-left: 70px;
      width: 520px;
      margin-top: 30px;
    }

    .me-chat{
      border: none;
      flex-wrap: wrap;
      padding: 10px;
      background: blue;
      text-align: right;
      color: white;
      border-top-right-radius: 8px;
      border-top-left-radius: 8px;
      border-bottom-left-radius: 8px;
      border-bottom-right-radius: 0px;
    }

    .bot-chat{
      border: none;
      padding: 10px;
      text-align: left;
      background:white;
      border-top-right-radius: 8px;
      border-top-left-radius: 8px;
      border-bottom-left-radius: 0px;
      border-bottom-right-radius: 8px;
    }

    .keyboard-chat{
      margin-top: 20px;
    }

    .btn-chat{
      border: none;
      background: none;
    }

    .date-some{
      position: absolute;
      top: -20px;
      right: 220px;
      font-size: 12px;
    }
    .date-me{
      position: absolute;
      top: -20px;
      right: 280px;
      font-size: 12px;
    }
  }

  @media (max-width: 384px) {
    .container{
      margin-top: -30px;
      margin-left: -30px;
      /* border-radius: 20px; */
      padding: 5px;
      /* border: 1px solid black; */
      width: 380px;
      height: 660px;
      background-size: cover;
    }

    .kerangka-title{
      background: blue;
      width: 386px;
      height: 70px;
      margin-top: -10px;
      margin-left: -10px;
    }

    .rangka-chat{
      /* border: 1px solid black; */
      height: 580px;
      position: relative;
      margin-top: 5px;
      overflow: auto;
    }

    .profile-avatar{
      margin-top: 10px;
      margin-left: 15px;
    }

    .title-name{
      margin-top: -50px;
      margin-left: 70px;
    }

    .sub-title-name{
      font-size: 10px;
      margin-top: -5px;
      margin-left: 70px;
    }

    .some-avatar{
      margin-top: 25px;
    }

    .me-chat{
      border: none;
      flex-wrap: wrap;
      padding: 10px;
      background: blue;
      text-align: right;
      color: white;
      border-top-right-radius: 8px;
      border-top-left-radius: 8px;
      border-bottom-left-radius: 8px;
      border-bottom-right-radius: 0px;
    }

    .bot-chat{
      border: none;
      padding: 10px;
      text-align: left;
      background:white;
      border-top-right-radius: 8px;
      border-top-left-radius: 8px;
      border-bottom-left-radius: 0px;
      border-bottom-right-radius: 8px;
    }

    .keyboard-chat{
      margin-top: 20px;
    }

    .btn-chat{
      border: none;
      background: none;
    }

    .date-some{
      position: absolute;
      top: -20px;
      right: 130px;
      font-size: 12px;
    }
    .date-me{
      position: absolute;
      top: -20px;
      right: 170px;
      font-size: 12px;
    }

    .cht-some{
      margin-top: -35px;
      margin-left: 40px;
      width: 280px;
      /* border: 1px solid black; */
      position: relative;
    }

    .cht-me{
      text-align: right;
      /* border: 1px solid black; */
      margin-left: 50px;
      width: 310px;
      margin-top: 30px;
    }

  }


</style>
