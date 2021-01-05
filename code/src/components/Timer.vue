<template>
    <div class="Timer">
        <!--  START BUTTON    -->
<button 
  id="start" 
  class="button is-dark is-large"
  @click="timeGoes(); toggleButtons();"> 
    <i class="far fa-play-circle"></i>
</button>

<!--   PAUSE BUTTON   -->
<button 
  id="stop" 
  class="button is-dark is-large"
  @click="timeStops(); toggleButtons();"
  > 
    <i class="far fa-pause-circle"></i>
</button>

<!--  RESET BUTTON   -->
<button 
  id="reset" 
  class="button is-dark is-large"
  @click="restartTimer"> 
    <i class="fas fa-undo"></i>
</button>

        <h2>{{phase}}: {{minutes}}:{{seconds}}</h2>
<br>
<h2>Next Steps</h2>
<ul>
    <li class="li">Include bootstrap-vue into project</li>
    <li class="li">Style home(work) page, add navigation (about, wim hof breath counter)</li>
    <li class="li">Learn NodeJs back-end -> create database, accounts, save and retrieve data to make it possible to keep track of progress</li>
    <li class="li">Give feedback on progress to make the app interactive and intelligent</li>
</ul>
    </div>

</template>
<script>
export default
{
    name: 'Timer',
    data(){
        return {
            timing: null,
            minutes: 0,
            seconds: 2,
            isWork: true,
            phase: "Work",
            audio: null
        }
    },
    methods: {
        timeGoes()
        {
            this.timing = setInterval(()=>{
            if(this.seconds > 0)
            {
                this.seconds--;
            }
            else
            {
                if(this.minutes > 0)
                {
                    this.seconds = 59;
                    this.minutes--;
                }
                else
                {
                    if(this.isWork)
                    {
                        this.minutes = 15;
                        this.phase = "Break";
                    }
                    else
                    {
                        this.minutes = 45;
                        this.phase = "Work";
                    }
                    this.timeEnds();
                }
            }
            }, 1000)
        },
        timeStops()
        {
            clearInterval(this.timing);
        },
        timeEnds()
        {
            if(this.isWork)
            {
                // we would like to add one star to today's achievements
                // and add to database that stores a list of days of each
                // month listing a day and deep work stars
                // users will be required
                // can do database and REST with node JS
            }
            // Trigger sound
            this.audio.play();
            this.isWork = !this.isWork;
        },
        restartTimer()
        {
            this.isWork = true;
            this.phase = "Work";
            this.toggleButtons();
            clearInterval(this.timing);
            this.minutes = 45;
            this.seconds = 0;
        },
        toggleButtons()
        {
            var startBtn = document.getElementById("start");
            var stopBtn = document.getElementById("stop");
            if(startBtn.style.display === "none")
            {
                startBtn.style.display = "inline";
                stopBtn.style.display = "none";
            }
            else
            {
                startBtn.style.display = "none";
                stopBtn.style.display = "inline";
            }
        }
    },
    mounted()
    {
        this.audio = new Audio(require('@/assets/gong.wav'))
    }
}
</script>

<style scoped>
.button{
    padding: 15px;
    font-size: 25px
}
#stop{
display: none
}
.li{
text-align: left;
margin:0;
padding:0;
}
</style>