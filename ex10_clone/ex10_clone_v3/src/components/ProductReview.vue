<template>
    <form class="review-form" @submit.prevent="onSubmit">

        <p class="error" v-if="errors.length">
        <b>Please correct the following error(s):</b>
        <ul>
            <li v-for="error in errors" :key="error.id">{{ error }}</li>
        </ul>
        </p>

        <p>
        <label for="name">Name:</label>
        <input id="name" v-model="name">
        </p>

        <p>
        <label for="review">Review:</label>
        <textarea id="review" v-model="review"></textarea>
        </p>

        <p>
        <label for="rating">Rating:</label>
        <select id="rating" v-model.number="rating">
            <option>5</option>
            <option>4</option>
            <option>3</option>
            <option>2</option>
            <option>1</option>
        </select>
        </p>

        <p>Would you recommend this product?</p>
        <label>
        Yes
        <input type="radio" value="Yes" v-model="recommend"/>
        </label>
        <label>
        No
        <input type="radio" value="No" v-model="recommend"/>
        </label>

        <p>
        <input type="submit" value="Submit">
        </p>

    </form>
</template>

<script>
export default {
    name: 'product-review',
    data() {
        return {
            name: null,
            review: null,
            rating: null,
            recommend: null,
            errors: []
        }
    },
    methods: {
        onSubmit() {
            this.errors = []
            if(this.name && this.review && this.rating && this.recommend) {
                let productReview = {
                name: this.name,
                review: this.review,
                rating: this.rating,
                recommend: this.recommend
                }
                this.$emit('review-submitted', productReview)
                // send up data from our child to our parent when an event occurs.
                // event name is 'review-submitted'.
                this.name = null
                this.review = null
                this.rating = null
                this.recommend = null
            } else {
                if(!this.name) this.errors.push("Name required.")
                if(!this.review) this.errors.push("Review required.")
                if(!this.rating) this.errors.push("Rating required.")
                if(!this.recommend) this.errors.push("Recommendation required.")
            }
        }
    }
}
</script>

<style scoped>
.review-form {
    width: 400px;
    padding: 20px;
    margin: 40px;
    border: 1px solid #d8d8d8;
}

input {
    width: 100%;
    height: 25px;
    margin-bottom: 20px;
}

textarea {
    width: 100%;
    height: 60px;
}

.tab {
    margin-left: 20px;
    cursor: pointer;
}

.activeTab {
    color: #16C0B0;
    text-decoration: underline;
}

</style>