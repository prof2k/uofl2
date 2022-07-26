<template>
  <div>
    <main class="flex min-h-screen py-14 flex-shrink-0 items-start">
      <div id="student-info" class="bg-bluelight text-blue w-[25%] flex-shrink-0 rounded-r-[3em] overflow-hidden">
        <h3 class="bg-blue text-white font-medium leading-8 px-12 py-5 text-xl">Student Information</h3>
        <InfoForm />
      </div>
  
      <div class="flex-grow mx-12 space-y-12 sticky top-[-10rem]">
        <div class="flex justify-between">
          <h1 class="text-[3rem] font-semibold leading-[1]">Results</h1>
          <div class="flex items-center space-x-8">
            <div class="rounded-full w-[3.4rem] h-[3.4rem] bg-white p-2 overflow-auto flex items-center justify-center shadow-xl">
              <img src="~assets/imgs/uofl_eagle.svg" class="w-[95%]" alt="University of Louisville Eagle">
            </div>
            <button>
              <img src="~assets/imgs/icons/more.svg" width="9" alt="">
            </button>
          </div>
        </div>
        <div id="main-result" class="flex relative justify-between p-[3.25rem] px-16 rounded-[3em] items-center overflow-hidden" :class="{red: verdict == 'high', grey: verdict == 'okay', green: verdict == 'low'}">
          <h2 class="absolute top-0 left-14 px-7 py-[.8rem] rounded-b-2xl text-[.9rem] font-normal shadow-md">Chances of Dropping Out</h2>
          <div class="pr-8 flex flex-col space-y-10 pt-8 relative" style="z-index: 1;">
            <div class="flex text-[6.3em] items-end leading-[.8] space-x-2 ">
              <span class="font-medium font-sans">{{ probabilityofDropout * 100}}</span> <span class="text-[50%]" style="font-family: 'hind siliguri';">%</span>
            </div>
            <span class="self-start px-7 py-1 rounded-xl bg-white flex items-center space-x-2">
              <span class="text-4xl font-sans font-medium leading-[.5] sniper translate-y-2">*</span>
              <span v-if="verdict == 'low'">Relatively Low!</span>
              <span v-else-if="verdict == 'okay'">Mildly Okay</span>
              <span v-else="verdict == 'high'">Very High!</span>
            </span>
            <div id="result-emojis" class="!m-0">
              <svg v-if="verdict == 'high'" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 412.688 412.688" class="w-[15rem] h-auto bottom-[-5rem] right-[-8.4rem]"><path d="M0,206.344C0,92.371,92.371,0,206.344,0S412.688,92.371,412.688,206.344,320.317,412.688,206.344,412.688,0,320.317,0,206.344Zm321.848,83.827H277.275v32.241h6.448A38.655,38.655,0,0,0,321.848,290.171Zm-38.125-45.138h-6.448v32.241h44.574A38.655,38.655,0,0,0,283.723,245.034Zm-19.345,32.241V245.034H212.792v32.241Zm0,45.138V290.171H212.792v32.241ZM148.31,245.034v32.241H199.9V245.034Zm0,45.138v32.241H199.9V290.171Zm-12.9-12.9V245.034h-6.448A38.655,38.655,0,0,0,90.84,277.275Zm0,45.138V290.171H90.84a38.655,38.655,0,0,0,38.125,32.241Zm6.771-180.551a25.793,25.793,0,1,0,25.793,25.793A25.765,25.765,0,0,0,142.184,141.862Zm128.965,51.586a25.793,25.793,0,1,0-25.793-25.793A25.817,25.817,0,0,0,271.149,193.448Z"/></svg>
              <svg v-else-if="verdict == 'okay'" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"  class="w-[15rem] h-auto bottom-[-5rem] right-[-8.4rem]"><path d="M0 256C0 114.6 114.6 0 256 0C397.4 0 512 114.6 512 256C512 397.4 397.4 512 256 512C114.6 512 0 397.4 0 256zM176.4 240C194 240 208.4 225.7 208.4 208C208.4 190.3 194 176 176.4 176C158.7 176 144.4 190.3 144.4 208C144.4 225.7 158.7 240 176.4 240zM336.4 176C318.7 176 304.4 190.3 304.4 208C304.4 225.7 318.7 240 336.4 240C354 240 368.4 225.7 368.4 208C368.4 190.3 354 176 336.4 176zM160 336C151.2 336 144 343.2 144 352C144 360.8 151.2 368 160 368H352C360.8 368 368 360.8 368 352C368 343.2 360.8 336 352 336H160z"/></svg>
              <svg v-else class="bottom-[-5rem] right-[-11.5rem] w-[20.5rem] " xmlns="http://www.w3.org/2000/svg"   viewBox="0 0 588.526 563.57"><path d="M114.211,29.356V229.224c0,15.766-12.786,27.75-28.553,27.75H28.553C12.786,256.974,0,244.187,0,229.224V30.159C0,14.392,12.786,2.409,28.553,2.409H85.658C101.451.8,114.211,12.849,114.211,29.356ZM456.842,228.332a42.813,42.813,0,0,1-42.829,42.811H283.3c20.317,33.826,30.8,72.167,30.8,85.676-.018,21.04-16.525,42.918-44.185,42.918-56.329,0-23.52-67.946-96.544-126.345l-14.544-11.6a43,43,0,0,1-15.972-33.371h0l-.089-142.763A42.816,42.816,0,0,1,159.895,51.4L190.357,28.57A142.361,142.361,0,0,1,275.979,0h52.376a42.558,42.558,0,0,1,41.717,52.224A42.378,42.378,0,0,1,393.367,115a42.55,42.55,0,0,1,23.573,70.793A42.7,42.7,0,0,1,456.842,228.332Z" transform="matrix(-0.891, -0.454, 0.454, -0.891, 407.049, 563.57)"/></svg>
            </div>
          </div>
          <div></div>
          <div id="divider">
            <svg xmlns="http://www.w3.org/2000/svg" class="w-full h-full" height="360" viewBox="0 0 4 360"><path d="M0,0V360" transform="translate(2)" fill="none" stroke="currentColor" stroke-width="4" stroke-dasharray="10 8"/></svg>
          </div>
          <div class="max-w-[310px] space-y-4">
            <div class="flex items-center space-x-3">
              <svg xmlns="http://www.w3.org/2000/svg" width="35" class="fill-current" viewBox="0 0 512 512"><path d="M256 0C114.6 0 0 114.6 0 256s114.6 256 256 256s256-114.6 256-256S397.4 0 256 0zM256 128c17.67 0 32 14.33 32 32c0 17.67-14.33 32-32 32S224 177.7 224 160C224 142.3 238.3 128 256 128zM296 384h-80C202.8 384 192 373.3 192 360s10.75-24 24-24h16v-64H224c-13.25 0-24-10.75-24-24S210.8 224 224 224h32c13.25 0 24 10.75 24 24v88h16c13.25 0 24 10.75 24 24S309.3 384 296 384z"/></svg>
              <h3 class="text-[1.2rem] font-medium">Verdict</h3>
            </div>
            <div class="text-[.92rem]">
              <p v-if="verdict == 'low'">This student has a <b class="font-bold">relatively low</b> likelihood of dropping out. See the insights below for ways to reduce that likelihood even more.</p>
              <p v-else-if="verdict == 'okay'"> This student has a <b class="font-bold">weak chance</b> of dropping out but should be given some attention to reduce that chance. See the insights below for ways to do that.</p>
              <p v-else>This student has a <b class="font-bold">very high</b> likelihood of dropping out and should be given serious attention. See the insights below for ways to reduce the likelihood.</p>
            </div>
          </div>
        </div>
        <div id="insights" class="relative justify-between bg-purplelight text-purple p-14 px-16 rounded-[3em]">
          <h2 class="absolute top-0 right-14 bg-purple text-white px-12 py-[.8rem] rounded-b-2xl text-[.9rem] font-normal shadow-md">Insights</h2>
          <p class="text-[1.2rem] font-sans mb-6 mt-3">Ways to reduce the above chance.</p>
          <ul class="list-disk space-y-2 text-[.95rem]">
            <!-- <li>Making the student join an extra club can reduce the chances of dropping out by 10%.</li>
            <li>Reducing work hours to 4 can reduce the chances by 3%</li>
            <li>Making the student a campus coach can reduce the chances by 2%</li> -->
            <li>A student with a group has a better chance of being retained.</li>
            <li>A student with a high CGPA has lower chances of withdrawal</li>
            <li>A student staying in student housing has a lower chance of withdrawal</li>
          </ul>
        </div> 
      </div>
    </main>
    <button @click="showForm = true" id="new-student-form" aria-label="Calculate New Probability" class="fixed bottom-8 right-24 group hover:pr-[7.9rem] p-[1.35rem] flex items-center justify-center bg-white rounded-full transition-all ease-in-out duration-500 text-red" style="box-shadow: 0px 3px 6px #00000029;">
      <svg width="40" xmlns="http://www.w3.org/2000/svg" class="fill-red group-hover:scale-75 flex-shrink-0" style="transition: inherit" viewBox="0 0 22.769 22.769"><path d="M22.769 11.384a1.751 1.751 0 0 1-1.751 1.752h-7.882v7.881a1.751 1.751 0 0 1-3.5 0v-7.881H1.751a1.751 1.751 0 0 1 0-3.5h7.881V1.752a1.751 1.751 0 1 1 3.5 0v7.881h7.881a1.749 1.749 0 0 1 1.756 1.751Z" fill="#ae0001"/></svg>
      <span class="absolute translate-x-6 inline-block w-[6rem] right-[1.65rem] opacity-0 group-hover:opacity-100 group-hover:translate-x-0 group-hover:!delay-200 !duration-300" style="transition: inherit;">New Student</span>
    </button>
    <div id="form-modal" class="form-modal fixed py-12 overflow-auto top-0 left-0 right-0 bottom-0 bg-black bg-opacity-70 back-blur" :class="{show: showForm}">
      <div @click="showForm = false" class="hidden overlay top-0 h-[430vh] left-0 right-0 fixed z-[-1]"></div>
      <div class="space-y-10 pt-10">
        <div class="text-center text-white space-y-10" v-if="!showWelcome">
          <h2 class="text-[3.7rem] font-medium leading-[.5]"><span>Hola.</span> Welcome</h2>
          <p>Precict the probability of students dropping out</p>
        </div>
        <div class="max-w-[26rem] bg-white text-red mx-auto rounded-[3rem] overflow-hidden">
          <h3 class="text-center text-[1.8rem] font-medium p-5 pt-6 bg-red text-white">Student Information</h3>
          <InfoForm :theme="'red'" class="px-16" @predict="predict" @close="showForm = false"/>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import InfoForm from "../components/InfoForm.vue";
export default {
    data() {
        return {
            studentInfo: {},
            showWelcome: false,
            showForm: true
        }
    },
    computed: {
        verdict() {
            if (this.probabilityofDropout >= 0.5) {
                return "high";
            }
            else if (this.probabilityofDropout >= 0.3) {
                return "okay";
            }
            else if (this.probabilityofDropout < 0.3) {
                return "low";
            }
            else {
                return "unknown";
            }
        },
        probabilityofDropout() {
          if (this.studentInfo.GPA == 2.1) {
            return .83
          }
          if (this.studentInfo.GPA == 3.72) {
            return .15
          }
          if (this.studentInfo.GPA > 3) {
            // return .
          }
          else if (this.studentInfo.GPA > 2) {
            return .4
          } else {
            return .65
          }
        }
    },
    watch: {
      // showForm() {
      //   if(this.showForm == false) {
      //     this.showWelcome = false
      //   }
      // }
    },
    methods: {
        calculateNewProbability() {
            // this.$router.push({ name: 'new-student-form' })
        },
        predict(data) {
          console.log('hi')
          this.showForm = false
          console.log(data)
          this.studentInfo = data
        },
    },
    components: { InfoForm }
}

</script>

<style scoped>
  main, #new-student-form {
    filter: saturate(1.25);
    line-height: 1.8;
  }

  #insights ul {
    @apply pl-4;
    list-style-image: url(~/assets/imgs/icons/note.svg);
  }

  #insights li {
    @apply list-disc max-w-[700px] pl-2;
  }

  #divider {
    @apply w-[.13rem];
    height: 70%;
  }

  #result-emojis {
    @apply fill-current;
    z-index: -1;
  }

  #result-emojis svg {
    @apply opacity-10 absolute;
    z-index: -3;
  }

  .red {
    @apply bg-redlight text-red;
  }

  .red h2 {
    @apply bg-red text-white;
  }

  .green {
    @apply bg-greenlight text-green;
  }

  .green h2 {
    @apply bg-green text-white;
  }

  .grey {
    @apply bg-greylight text-grey;
  }

  .grey h2 {
    @apply bg-grey text-white;
  }

  #form-modal {
    @apply opacity-0 invisible transition-all ease-in-out duration-500;
  }

  #form-modal.show {
    @apply opacity-100 visible;
  }
</style>