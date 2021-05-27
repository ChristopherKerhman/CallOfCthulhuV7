

<template>
  <html lang="fr" dir="ltr">
    <head>
      <meta charset="utf-8">
      <title>L'appel de Cthulhu - Application V-7</title>
    </head>
    <body class="transition">
      <header>
        <div class="CAlignCenter">
        <h1>L'appel de Cthulhu</h1>
        <h2 class="sous_titre">Test de compétence pour L'appel de Cthulhu JDR V.7</h2>
      </div>
      </header>
      <section>
        <article class="centre">
        <p class="paragraphe1"><span><button v-if="!majeur || !extreme || !normal" id="clair" type="button" v-on:click="zero">X</button></span>Compétance de l'investigateur : <input class="size" type="number" name="competance" v-model="competance" /> %</p>
        </article>
        <article id="testButton" class="centre">
          <button v-if="normal" class="B_test" id="clair" type="button" name="button" v-on:click="choixO">Test ordinaire</button>
          <button v-else class="B_test no" id="clair" type="button" name="button">Test ordinaire</button>
          <button v-if="majeur" class="B_test" id="sombre" type="button" name="button" v-on:click="choixM">Test majeur</button>
          <button v-else class="B_test no" id="sombre" type="button" name="button">Test majeur</button>
          <button v-if="extreme" class="B_test" id="dark" type="button" name="button" v-on:click="choixE">Test extrême</button>
          <button v-else class="B_test no" id="dark" type="button" name="button">Test extrême</button>
        </article>
      </section>
      <section>
        <article class="box">
          <button class="d100" v-on:click="oneDice">1D100</button>
          <div class="dice_box">
            <button class="d100" v-on:click="twoDice(1, true)">1 D 100<br />+1D bonus</button>
            <button class="d100" v-on:click="twoDice(2, true)">1 D 100<br />+2D bonus</button>
          </div>
          <div class="dice_box">
            <button class="d100" v-on:click="twoDice(1, false)">1 D 100<br />+1D malus</button>
            <button class="d100" v-on:click="twoDice(2, false)">1 D 100<br />+2D malus</button>
          </div>
        </article>
        <article class="bottle transition" v-if="message != ''">
          <p>{{message}} <span v-if="this.normal && this.majeur && this.extreme"></span><span v-else>{{competance}}%</span></p>
        </article>
      </section>
    </body>
  </html>
</template>
<script>
export default {
  name: 'App',
  data () {
    return {
      competance: 0,
      message: '',
      typeR: '',
      // Divers choix
      normal: true,
      majeur: true,
      extreme: true,
      bonus: false,
      malus: false
    }
  },
  methods: {
    zero () {
      this.normal = true
      this.majeur = true
      this.extreme = true
      this.competance = 0
      this.message = ''
    },
    choixO () {
      this.normal = true
      this.majeur = false
      this.extreme = false
    },
    choixM () {
      this.normal = false
      this.majeur = true
      this.extreme = false
    },
    choixE () {
      this.normal = false
      this.majeur = false
      this.extreme = true
    },
    testO (D100) {
      // Test simple
      if (D100 === 1) {
        this.message = `Réussite critique avec ${D100}%/`
      } else if (D100 <= this.competance) {
        this.message = `Réussite avec ${D100}%/`
      } else if (D100 > 95) {
        this.message = `Maladresse avec ${D100}%/`
      } else {
        this.message = `Echec avec ${D100}%/`
      }
    },
    testM (D100) {
      // Test simple
      if (D100 === 1) {
        this.message = `Test majeur: réussite critique avec ${D100}%/`
      } else if (D100 <= this.competance / 2) {
        this.message = `Test majeur: réussite avec ${D100}%/`
      } else if (D100 > 95) {
        this.message = `Maladresse avec ${D100}%/`
      } else {
        this.message = `Echec avec ${D100}%/`
      }
    },
    testE (D100) {
      // Test simple
      if (D100 === 1) {
        this.message = `Test extrême: réussite critique avec ${D100}%/`
      } else if (D100 <= this.competance / 5) {
        this.message = `Test extrême: réussite avec ${D100}%/`
      } else if (D100 > 95) {
        this.message = `Maladresse avec ${D100}% /`
      } else {
        this.message = `Echec avec ${D100}% /`
      }
    },
    oneDice () {
      if (this.normal && this.majeur && this.extreme) {
        this.message = 'Valider un test pour lancer l\'opération.'
      } else {
      if (this.normal) {
        const DK = Math.floor((Math.random() * 100) + 1)
        this.testO(DK)
      }
      if (this.majeur) {
        const DK = Math.floor((Math.random() * 100) + 1)
        this.testM(DK)
      }
      if (this.extreme) {
        const DK = Math.floor((Math.random() * 100) + 1)
        this.testE(DK)
      }
      }
    },
    twoDice (k, ted) {
      if (this.normal && this.majeur && this.extreme) {
        this.message = 'Valider un test pour lancer l\'opération.'
      } else {
      const jet = []
      for (let charlie = 0; charlie <= k; charlie++) {
        const DD = Math.floor((Math.random() * 100) + 1)
        jet.push(DD)
      }
      jet.sort(function (a, b) {
        return a - b
      })
      console.log(jet)
      let DK = 0
      console.log(DK)
      if (!ted) {
        const lastDice = jet.length
        DK = jet.[lastDice - 1]
      } else {
        DK = jet.[0]
      }
      if (this.normal) {
        this.testO(DK)
      } else if (this.majeur) {
        this.testM(DK)
      } else {
        this.testE(DK)
      }
      }
    }
  }
}
</script>

<style>
/* Font pour le site web */
/*==Titre de l'application==*/
@import url('https://fonts.googleapis.com/css2?family=Parisienne&display=swap');

body {
  background-color: #1B3A4B;
  color: black;
  max-height: 100%;
}
/*==Les boites==*/
.CAlignCenter {
  display: flex;
  flex-direction: column;
  background-color: #157172;
  border-radius: 60px;
  border: 4px groove #441E44;
}
.box {
  display: flex;
  flex-direction: column;
  padding-bottom: 1.5em;
}
.dice_box {
  display: flex;
  flex-direction: row;
}
.bottle {
  display: block;
  margin: auto;
  height: 2.3em;
  width: 97%;
  background-color: #57cc99;
  border-radius: 60px;
  border: 4px groove #441E44;
  text-align: center;
  font-size: 1em;
}
/*==Presentation==*/
h1 {
  font-family: 'Parisienne', cursive;
  font-size: 2em;
  text-align: center;
  margin-bottom: 0em;
  margin-top: 0.2em;
}
.paragraphe1 {
  font-size: 0.9em;
}
.sous_titre {
  margin-top: 0em;
  text-align: center;
  font-size: 0.5em;
}
.centre {
  text-align: center;
  font-size: 1em;
  color: black;
  height: 25%;
}
.size {
  border-radius: 10px;
  border: 4px groove #441E44;
  width: 20%;
  height: 2em;
  text-align: center;
}
/*==Les boutons==*/
#testButton {
  display: flex;
  flex-direction: column;
}

.B_test {
  display: block;
  margin: auto;
  height: 100%;
  width: 45%;
  border-radius: 50px;
  border: 3px solid black;
  font-size: 1em;
  margin-bottom: 1em;
  color: black;
}
.no {
  text-decoration: line-through;
}
.d100 {
  margin-bottom: 0.5em;
  margin: auto;
  font-size: 1em;
  height: 5em;
  width: 5em;
  color: black;
  display:block;
  text-decoration:none;
  margin:5px auto;
  border-radius:5px;
  border:solid 1px #272640;
  background-color: #0B525B;
  text-align:center;
  padding: auto;
  -webkit-transition: all 0.1s;
  -moz-transition: all 0.1s;
  transition: all 0.1s;
  -webkit-box-shadow: 0px 9px 0px #84261a;
  -moz-box-shadow: 0px 9px 0px #84261a;
  box-shadow: 0px 9px 0px #441E44;
}
.d100:active {
  -webkit-box-shadow: 0px 2px 0px #84261a;
    -moz-box-shadow: 0px 2px 0px #84261a;
    box-shadow: 0px 2px 0px #441E44;
    position:relative;
    top:7px;
}
.d100:hover {
  background-color: #00b914;
}

#clair {
  background-color: #157172;
}
#sombre {
  background-color: #272640;
  color: #a3ffe2;
}
#dark {
  background-color: #8e078e;
  color: #a3ffe2;
}
/*===Effet spéciaux=*/
.transition {
  animation-duration: 3s;
  animation-name: slidein;
  animation-direction: normal;
}
@keyframes slidein {
  from {
    margin-left: 100%;
    width: 300%;
  }

  to {
    margin-left: 0%;
    width: 100%;
  }
}
</style>
