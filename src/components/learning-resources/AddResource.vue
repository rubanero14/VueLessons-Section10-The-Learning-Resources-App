<template>
    <base-dialog v-if="inputIsInvalid" title="Invalid Input!" @close="closeDialog">
        <template #default>
            <p class="text-danger"><strong><em>Please dont leave any input field blank!</em></strong></p>
            <p>Kindly check all the inputs and make sure its not empty.</p>
        </template>
        <template #actions>
            <base-button class="btn link" @click="closeDialog">OK</base-button>
        </template>
    </base-dialog>
    <base-card>
        <h2>Add Resource</h2>
        <form @submit.prevent="submitData">
            <div class="form-margin">
                <label for="title">Title</label>
                <input id="title" name="title" type="text" ref="titleInput">
            </div>
            <div class="form-margin">
                <label for="description">Description</label>
                <textarea name="description" id="description" rows="3" ref="descInput"></textarea>
            </div>
            <div class="form-margin">
                <label for="link">Link</label>
                <input id="link" name="link" type="url" ref="linkInput">
            </div>
            <div>
                <base-button class="btn btn-purple" type="submit">Add Resource</base-button>
            </div>
        </form>
    </base-card>
</template>

<script>
export default {
    inject: ['addResource'],
    data(){
        return {
            inputIsInvalid: false,
        };
    },
    methods: {
        submitData(){
            const enteredTitle = this.$refs.titleInput.value;
            const enteredDesc = this.$refs.descInput.value;
            const enteredLink = this.$refs.linkInput.value;
            
            if(enteredTitle.trim() === '' || 
               enteredDesc.trim() === '' || 
               enteredLink.trim() === ''){
                this.inputIsInvalid = true;
                return;
            }

            this.addResource(enteredTitle, enteredDesc, enteredLink);
        },
        closeDialog() {
            this.inputIsInvalid = false;
        }
    },
}
</script>

<style scoped>
.form-margin {
    margin: 1rem 0;
}

input:focus, textarea:focus {
    outline: none;
    border-color: #3a0061;
    background: #f7ebff;
}

input, textarea {
    display: block;
    width: 100%;
    font: inherit;
    padding: 0.15rem;
    border: 1px solid #ccc;
    border-radius: 4px;
}

label {
    font-weight: bold;
    display: block;
    margin-bottom: 0.5rem;
}

button.link {
    text-decoration: none;
    background-color: #D2AC47;
    color: #fff;
    box-shadow: none;
}

button.link:hover, button.link:active {
    background-color: #AE8625;
    color: #fff;
}
</style>
