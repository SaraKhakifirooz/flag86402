<template class="dark">
    <!-- <div>
        <div>Count: {{ count }}</div>
        <div>isActive: {{ isActive }}</div>
        <div>
            <button @click="pause">
                pause
            </button>
            <button @click="resume">
                resume
            </button>
        </div>
    </div> -->
    <div @click="isDark">
        isDark
    </div>
    <button @click="toggleDark()">
        <span class="ml-2">{{ isDark ? 'Dark' : 'Light' }}</span>
    </button>
    <div class="flex items-center justify-center h-[100vh] overflow-hidden transition transition-all delay-50">


        <div class="w-[30%] bg-gray-200 h-full flex items-center justify-center text-center m-auto transition transition-all delay-50 validateEmail"
            :class="[hitTomato ? 'ml-[-15%]' : '', '']">
            <div>
                <div class="text-center m-auto cursor-pointer" @click="hitKon">
                    <svg class="w-[150px] bg-red-500 rounded-full p-5" viewBox="-1 0 12 12" version="1.1"
                        xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" fill="#000000">
                        <g id="SVGRepo_bgCarrier" stroke-width="0"></g>
                        <g id="SVGRepo_tracerCarrier" stroke-linecap="round" stroke-linejoin="round"></g>
                        <g id="SVGRepo_iconCarrier">
                            <title>play [#1000]</title>
                            <desc>Created with Sketch.</desc>
                            <defs> </defs>
                            <g id="Page-1" stroke="none" stroke-width="1" fill="none" fill-rule="evenodd">
                                <g id="Dribbble-Light-Preview" transform="translate(-65.000000, -3803.000000)"
                                    fill="#000000">
                                    <g id="icons" transform="translate(56.000000, 160.000000)">
                                        <path
                                            d="M18.074,3650.7335 L12.308,3654.6315 C10.903,3655.5815 9,3654.5835 9,3652.8985 L9,3645.1015 C9,3643.4155 10.903,3642.4185 12.308,3643.3685 L18.074,3647.2665 C19.306,3648.0995 19.306,3649.9005 18.074,3650.7335"
                                            id="play-[#1000]"> </path>
                                    </g>
                                </g>
                            </g>
                        </g>
                    </svg>
                </div>
                <div class="text-[5rem]">
                    <h1> {{ timedown }}</h1>
                </div>
            </div>
        </div>
        <div v-show="hitTomato"
            class="w-[70%] h-full flex items-center justify-center bg-gray-100 transition transition-all delay-150"
            :class="[hitTomato ? 'w-[85%]' : '', 'w-[70%]']">

            <div>
                <h1 class="text-[30px]">New Task</h1>
                <br />
                <pomodoroInput v-model="user.name" label="name" type="text" />
                <pomodoroInput v-model="user.email" label="email" id="emailvalid" type="email" />
                <div>
                    <button @click="checkvalid()"
                        class="bg-gray-500 text-white text-[20px] rounded-full w-full mt-3">Start</button>
                </div>
                <div>
                    <button @click="cancel"
                        class="bg-gray-400 text-white text-[20px] rounded-full w-full mt-3">Cancel</button>
                </div>
            </div>
        </div>
        <div class="w-[70%] h-full flex items-center justify-center transition transition-all delay-150"
            v-show="!hitTomato">
            <div class="rounded-full w-[100px] h-[100px] flex items-center justify-center">
                <svg width="100px" fill="#ddd" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                    <g id="SVGRepo_bgCarrier" stroke-width="0"></g>
                    <g id="SVGRepo_tracerCarrier" stroke-linecap="round" stroke-linejoin="round"></g>
                    <g id="SVGRepo_iconCarrier">
                        <path
                            d="M20 3H4M20 21H4M5 3C5 5.51022 6.21228 7.86592 8.25493 9.32495L15.7451 14.675C17.7877 16.1341 19 18.4898 19 21M19 3C19 5.51022 17.7877 7.86592 15.7451 9.32495L8.25493 14.675C6.21228 16.1341 5 18.4898 5 21"
                            stroke="#000000" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"></path>
                    </g>
                </svg>
            </div>
        </div>
    </div>
</template>


<script setup>
import { useTimeoutPoll } from '@vueuse/core'
import { useTitle, useDark, useToggle, useColorMode } from '@vueuse/core'

const hitTomato = ref(false)
const timedown = ref(10)
const count = ref(0)
const user = ref({
    name: '',
    email: '',
})
const reg = ref(/^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,24}))$/)

const hitKon = () => {
    hitTomato.value = true;
}

const mode = useColorMode()


const isDark = useDark()
const toggleDark = useToggle(isDark)

const title = computed(() => isDark.value ? '🌙 Good evening!' : '☀️ Good morning!')

console.log(useTitle(title))

watch(isDark, (newVal) => {
    // toggle the 'dark' class on the documentElement after a delay
    setTimeout(() => {
        document.documentElement.classList.toggle('dark', newVal);
    }, 150);
});

// async function fetchData() {
//     await new Promise(resolve => setTimeout(resolve, 1000))
//     count.value++
// }

// const { isActive, pause, resume } = useTimeoutPoll(fetchData, 1000)

const cancel = () => {
    user.value.name = '';
    user.value.email = '';
}

const toggleClassActive = () => {
    // از این میخواستم استفاده کنم واسه تاگل شدن کلاس که عقب جلو بره 
    hitTomato.value = !hitTomato.value;
}

const countdown = () => {
    timedown.value--;
    if (timedown.value > 0) {
        setTimeout(countdown, 1000);
    }
    if (timedown.value == 0) {
        alert("Time Is Up");
    }
}

const checkvalid = () => {
    if (validName() && validateEmail()) {
        countdown()

        //این کار نمیکنه نمیدونم چرا
        this.content['validateEmail'] ? 'w-[30%]' : '';
    }
}

const validName = () => {
    if (user.value.name = "") {
        alert('Enter Your Name')
    }
    else {
        return true
    }
}

const validateEmail = () => {
    if (!(/^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/.test(user.value.email))) {
        alert('Please enter a validdd email address')
    }
    else if (user.value.name = "") {
        alert('Please enter an email address')
    }
    else {
        return true
    }
}

</script>