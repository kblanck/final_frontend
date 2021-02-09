<template>
    <details><summary>Edit</summary>
              <form @submit="updateGlasses" method="post">
                <label htmlFor="name">Name</label>
                <br />
                <input
                  type="text"
                  id="name"
                    :placeholder="glass.name"
                    :v-model="updatedGlasses.name"
                />
                <br />
                <label htmlFor="price">Price</label>
                <br />
                <input
                  type="text"
                  id="price"
                    :placeholder="glass.price"
                    :v-model="updatedGlasses.price"
                />
                <br />
                <label htmlFor="description">Description</label>
                <br />
                <input
                  type="text"
                  id="description"
                    :placeholder="glass.description"
                    :v-model="updatedGlasses.description"
                />
                <br />
                <button type="submit">Edit</button>
              </form>
            </details>
</template>

<script>
import axios from 'axios'

export default {
    name: 'Update Glasses',
    data() {
        return {
            newGlasses: {
                name: null,
                price: null,
                description: null
            }
        }
    },
    methods: {
        updateGlasses(id) {
            axios.put('http://localhost:8080/glasses/' + id)
            .then(response => {
                this.updatedGlasses.name = response.data.name
                this.updatedGlasses.price = response.data.price
                this.updatedGlasses.description = response.data.description
                this.glasses.push(this.updatedGlasses)
            })
        } 
    },
}
</script>