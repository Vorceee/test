<template>
    <div>
        <div class="tab">
            <div id="app">
                <div>
                    <div class="centerComponent">
                        <h2>Overall rating:</h2>
                        <div class="rating">
                            <span v-for="star in 5" :key="star" @click="setRating(star)"
                                :class="{ 'rated': star <= currentRating, 'unrated': star > currentRating }">
                                ★
                            </span>
                        </div>
                        <!-- only show this when localstorage key program is not stretching -->
                        <p v-if="program !== 'Stretching'">Your difficulty rating for the {{ program }} program was: </p>
                        <p v-if="program !== 'Stretching'" class="difficultyLevel">{{ getProgramDifficultyRating(program)
                        }}/5</p>
                        <button class="submitButton" @click="submitRating">Submit</button>
                    </div>
                </div>

                <div id="footer">
                </div>
            </div>
        </div>
    </div>
</template>
  
<script>
export default {
    data() {
        return {
            currentRating: 0,
            program: '',
            WeightsDifficultyRating: 0,
            HIITDifficultyRating: 0,
            CalisthenicsDifficultyRating: 0,
        };
    },
    mounted() {
        this.program = localStorage.getItem('program') || '';

        this.WeightsDifficultyRating = parseInt(localStorage.getItem('WeightsDifficultyRating')) || 1;
        this.HIITDifficultyRating = parseInt(localStorage.getItem('HIITDifficultyRating')) || 1;
        this.CalisthenicsDifficultyRating = parseInt(localStorage.getItem('CalisthenicsDifficultyRating')) || 1;
    },
    methods: {
        setRating(rating) {
            this.currentRating = rating;
        },
        getProgramDifficultyRating(program) {
            switch (program) {
                case 'Weights':
                    return this.WeightsDifficultyRating;
                case 'HIIT':
                    return this.HIITDifficultyRating;
                case 'Calisthenics':
                    return this.CalisthenicsDifficultyRating;
                default:
                    return 0;
            }
        },
        submitRating() {
            if (this.currentRating === 0) {
                return;
            }
            else if (this.currentRating === 5 && this.getProgramDifficultyRating(this.program) < 5) {
                this[this.program + 'DifficultyRating']++;
                localStorage.setItem(`${this.program}DifficultyRating`, this.getProgramDifficultyRating(this.program));
            }

            else if (this.currentRating < 3 && this.getProgramDifficultyRating(this.program) > 1) {
                this[this.program + 'DifficultyRating']--;
                localStorage.setItem(`${this.program}DifficultyRating`, this.getProgramDifficultyRating(this.program));
            }
            window.location.href = '/programchoices';
        },
    },
};
</script>
  
<style>
p {
    font-size: 30px;
    margin-top: 2rem;
    margin-bottom: 2rem;
}

.difficultyLevel {
    font-size: 50px;
    margin-top: 1rem;
    margin-bottom: 1rem;
    font-weight: 600;
}

.rating {
    font-size: 100px;
    cursor: pointer;
}

.rated {
    color: orange;
}
</style>
  