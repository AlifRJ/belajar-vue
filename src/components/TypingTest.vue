<!--

Logic:

*) Get user input from input box, store to variable
*) Compare variable to word list ([] spit)
*) Make variable for amount of wrong(error) words and typed words
*) if: user pressed space, higlight the word(text) green and typed += 1/ else if: wrong and user pressed space, highligt the word(text) red, var wrong += 1 and typed += 1
    -- maybe check per character? instead of words?
*) To calculate wpm & accuracy: https://www.speedtypingonline.com/typing-equations

-->

<!-- 
=====================   
        Setup 
=====================
 -->

<script setup>

// +++++ Text view (show n amount of words) +++++

    let spit = []

    // list of 100 English common words
    const words = ref([
        "time", "year", "people", "way", "day", "man", "thing", "woman", "life", "child", "world", "school", "state", "family", "student", "group", "country", "problem", 
        "hand", "part", "place", "case", "week", "company", "system", "program", "question", "work", "government", "number", "night", "point", "home", "water", "room", 
        "mother", "area", "money", "story", "fact", "month", "lot", "right", "study", "book", "eye", "job", "word", "business", "issue", "side", "kind", "head", "house", 
        "service", "friend", "father", "power", "hour", "game", "line", "end", "member", "law", "car", "city", "community", "name", "president", "team", "minute", "idea", 
        "kid", "body", "information", "back", "parent", "face", "others", "level", "office", "door", "health", "person", "art", "war", "history", "party", "result", "change", 
        "morning", "reason", "research", "girl", "guy", "moment", "air", "teacher", "force", "education"
    ])
    // list of English common conjucntion
    const conjunction = ref([
        "and", "that", "but", "or", "as", "if", "when", "than", "because", "while", "where", "after", "so", "though", "since", "until", "whether", "before", "although", "nor", 
        "like", "once", "unless", "now", "except"
    ])

    // Get n words randomly
    function commonWords(n){
        for (let i = 0; i<n/2; i++) {
            let randomWords = Math.floor(Math.random()*words.value.length) 
            let randomConjunction  = Math.floor(Math.random()*conjunction.value.length)
            spit.push(words.value[randomWords])
            spit.push(conjunction.value[randomConjunction])
        }
    }

    commonWords(200)

// +++++ Inputs (inputbox and buttons) +++++

    import { ref } from "vue"

    const time = ref(60)
    const text = ref("")

    // timer function
    function CountDown(){
    if (time.value > 0){
        time.value--  
        // ! use date time insted of decrement number !
        setTimeout(CountDown, 1000) 
    } 
    }

    // input reset
    function reset() {
    text.value = ''
    }

// +++++ Typing test logic +++++

</script>

<!-- 
=====================   
      Template 
=====================
 -->

<template>
    <div class="container mx-auto p-2">
        <span v-for="word in spit">
            {{ word+' ' }} 
        </span>
    </div>
    <br>

    <div class="container input-group mb-3">
        <!-- Input  -->
        <input class="form-control" v-model="text" @keypress.space="reset" placeholder="Type here">
        <!-- Count Down Timer -->
        <span class="input-group-text">
          <p>Time: {{ time }}</p>
        </span>
    </div>

    <div class="container">
      <a type="button" class="btn btn-primary" href="/">Reset</a>
      <button type="button" class="btn btn-primary" @click="CountDown">Start</button>
    </div>
</template>