<template>
    <div>
        <div class="tab">
            <div id="app">
                <div id="header">
                    <usertitle v-model="text" text="Welcome "></usertitle>
                </div>
                <div id="body">
                    <h2>Select an exercise plan:</h2>

                    <div id="row">
                        <a v-for="choice in programChoices" :key="choice.program" :href="choice.link" id="link"
                            @click.prevent="saveProgram(choice.program)">
                            <div id="program">
                                <img :src="choice.image" alt="program icon" />
                                <h1>{{ choice.program }}</h1>
                            </div>
                        </a>
                    </div>
                    <div class="musicContainer">
                        <p id="chooseMusic">Choose your music</p>
                        <musicdropdown></musicdropdown>
                    </div>
                </div>
                <div id="footer">
                </div>
            </div>
        </div>
    </div>
</template>
  
<script>
import musicdropdown from './musicdropdown.vue';
import usertitle from './userTitle.vue';
export default {
    data() {
        return {
            programChoices: [
                {
                    link: '/programpreview',
                    image: '/src/assets/HIIT.svg',
                    program: 'HIIT',
                },
                {
                    link: '/programpreview',
                    image: '/src/assets/weights.svg',
                    program: 'Weights',
                },
                {
                    link: '/programpreview',
                    image: '/src/assets/calisthenics.svg',
                    program: 'Calisthenics',
                },
                {
                    link: '/programpreview',
                    image: '/src/assets/stretching.svg',
                    program: 'Stretching',
                },
                // Add more program choices here
            ],
        };
    },
    components: {
        musicdropdown,
        usertitle,
    },
    props: {
        link: {
            type: String,
            required: true
        },
        image: {
            type: String,
            required: true
        },
        program: {
            type: String,
            required: true
        }
    },
    methods: {
        saveProgram(program) {
            localStorage.setItem('program', program);
            window.location.href = '/programpreview';
        }
    }
}
</script>

<style>
#link {
    text-decoration: none;
}

#program {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    width: 15vw;
    height: 40vh;
    border: 1px solid rgb(134, 134, 134);
    border-radius: 10px;
    background-color: rgb(250, 250, 250);
    transition: 0.3s;
}

#program:hover {
    animation: shake 0.5s;
    animation-iteration-count: infinite;
    cursor: pointer;
    box-shadow: 0px 0px 10px 0px rgba(0, 0, 0, 0.75);
}

@keyframes shake {
    0% {
        transform: translate(0, 0);
    }

    50% {
        transform: translate(0, -10px);
    }

    100% {
        transform: translate(0, 0);
    }
}

#program h1 {
    font-size: 1.5vw;
    font-weight: bold;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    color: rgb(0, 0, 0);
    margin-top: 10vh;

}

#program img {
    width: 10vw;
    height: 20vh;
    margin-top: 2vh;
    outline: none;
    background-color: transparent;
}

#program h1 {
    font-size: 1.5vw;
    font-weight: bold;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    color: rgb(0, 0, 0);
    margin-top: 10vh;

}

#program img {
    width: 10vw;
    height: 20vh;
    margin-top: 2vh;
}
</style>
