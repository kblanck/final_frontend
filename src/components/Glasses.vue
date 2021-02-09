<template>
        <h1>DORBY BARKER</h1>

        <img id="splash" src="https://images.pexels.com/photos/2710178/pexels-photo-2710178.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=650&w=940">

        <div class="main-container">
            <div id="glasses-div" v-for="glass in glasses" :key="glass.id">
                <h3>{{ glass.name }}</h3>
                <h4>${{ glass.price }}</h4>
                    {{ glass.description }}
                <br/>
                
                <details><summary>Edit</summary>
              <form @submit="updateGlasses" :id="glass.id" method="put">
                <label htmlFor="name">Name</label>
                <br />
                <input
                  type="text"
                    :v-model="updatedGlasses.name"
                />
                <br />
                <label htmlFor="price">Price</label>
                <br />
                <input
                  type="text"
                    :v-model="updatedGlasses.price"
                />
                <br />
                <label htmlFor="description">Description</label>
                <br />
                <input
                  type="text"
                    :v-model="updatedGlasses.description"
                />
                <br />
                <button type="submit">Edit</button>
              </form>
            </details>

                <button class="button" id="delete-button" v-on:click="deleteGlasses(glass.id)">
                    Delete
                </button>
            </div>
            
            </div>

</template>

<script>
import axios from 'axios'

export default {
    name: 'Glasses',
    data() {
        return {
            glasses: [],
            updatedGlasses: {
                name: null,
                price: null,
                description: null
            }
        }
    },
    methods: {
        getGlasses() {
            axios.get('http://localhost:3000/glasses')
            .then(response => {
                this.glasses = response.data;
            })
            .catch(error => {
                console.log(error)
            })
        },
        deleteGlasses(id) {
            if (confirm("Are you sure you want to delete?")) {
                axios.delete('http://localhost:3000/glasses/' + id)
                .then((response) => {
                    this.getGlasses();
                })
            } else {
                return;
            }
        },
        updateGlasses(event) {
            console.log('test')
            event.preventDefault();
            const id = event.target.id
            axios.put('http://localhost:3000/glasses/' + id, this.updatedGlasses)
            .then(response => {
                console.log(response)
                this.getGlasses();
            }).catch(error => {
                console.log(error.message)
            })
        }
    },
    mounted() {
            this.getGlasses()
        }
}
</script>

<style scoped>

#splash {
    width: 95vw;
    border-radius: 3px;
}

.main-container {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
}

#glasses-div {
    width: 20vw;
    padding: 1em;
    margin: 1em;
    border: 1px solid rgb(194, 194, 194);
    border-radius: 5px;
}

h1 {
    padding-top: 0; 
    margin-top: 0;
    letter-spacing: .3em;
}

h3, h4 {
    margin: 0;
    padding: 0;
}

#edit-button {
    background-color: #eee;
    color: #2c3e50;
    border: 1px solid #2c3e50;
    border-radius: 3px;
    margin: .5em;
}

#delete-button {
    background-color: red;
    color: white;
    border: 1px solid red;
    border-radius: 3px;
}

</style>