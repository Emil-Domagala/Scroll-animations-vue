<template>
    <form @submit.prevent='submitHandler' id="waitlistForm" class="launchlist-form" method="post" target="_blank">
        <div class="input">
            <label for='nameField'>Name</label>
            <input type="text" name="name" placeholder="Cool Person" id="nameField" v-model.trim='name.value'
                @keyup='onChangeName()'>
            <p v-if='name.isValid === false'>Please check if provided data is correct</p>
        </div>
        <div class="input">
            <label for='emailField'>Email</label>
            <input type="email" name="email" placeholder="you@cool.site" id="emailField" v-model.trim='email.value'
                @keyup='onChangeEmail()'>
            <p v-if='email.isValid === false'>Please check if provided data is correct</p>
        </div>
        <div class="input">
            <label for='role'>Role</label>
            <select id='role' name="role" v-model.trim='role.value'>
                <option value="fullstack">Fullstack Developer</option>
                <option value="backend">Backend Developer</option>
                <option value="frontend">Frontend Developer</option>
                <option value="designer">Designer</option>
                <option value="product">Product</option>
                <option value="founder">Founder</option>
                <option value="other">Other</option>
            </select>
        </div>
        <div class="submit">
            <button>Join Waitlist</button>
        </div>




        <Modal title='Your message was send' message='We will contact with you as soon as we launch' button='Ok!'
            @close='closeModal' :isVisible='isModalVisible'></Modal>





    </form>
</template>

<script>
import Modal from '../../modal/modal.vue'
export default {
    components: {
        Modal,
    },
    data() {
        return {
            name: {
                value: '',
                isValid: null
            },
            email: {
                value: '',
                isValid: null
            },
            role: {
                value: 'fullstack',
                isValid: null
            },
            formWasClicked: false,
            isModalVisible: false,
        }
    },
    methods: {
        closeModal() {
            this.isModalVisible = false
            console.log('works')
        },
        onChangeName() {
            if (!this.formWasClicked) {
                return
            }
            if (this.name.value !== '') {
                this.name.isValid = true
                return
            }
            this.name.isValid = false
        },
        onChangeEmail() {
            if (!this.formWasClicked) {
                return
            }
            if (this.email.value !== '' && this.email.value.includes('@')) {
                this.email.isValid = true
                return
            }
            this.email.isValid = false
        },
        validataName() {
            if (this.name.value !== '') {
                this.name.isValid = true
                return
            }
            this.name.isValid = false
        },
        validataEmail() {
            if (this.email.value !== '' && this.email.value.includes('@')) {
                this.email.isValid = true
                return
            }
            this.email.isValid = false
        },
        validataRole() {
            if (this.role.value !== '') {
                this.role.isValid = true
                return
            }
            this.role.isValid = false
        },

        submitHandler() {
            this.formWasClicked = true
            this.validataName(), this.validataEmail(), this.validataRole()
            if (this.name.isValid !== true || this.email.isValid !== true || this.role.isValid !== true) {
                return
            }
            this.isModalVisible = true;
            this.clearInputs()
        },
        clearInputs() {
            this.name.value = ''
            this.name.isValid = null
            this.email.value = ''
            this.email.isValid = null
            this.role.value = 'fullstack'
            this.role.isValid = null
            this.formWasClicked = false
        }
    }
}
</script>

<style scoped lang='scss'>
form {
    padding: 0px;
    width: 80%;
    text-align: left;
    background: #FFFFFF;
    font-size: 14px;
    box-shadow: 0px 0px 1px rgba(0, 0, 0, 0.25), 0px 15px 60px rgba(0, 0, 0, 0.15), 0px 5px 7px rgba(0, 0, 0, 0.05), 0px 4px 20px rgba(0, 0, 0, 0.04);
    border-radius: 10px;
    z-index: 1;
    transform: translateX(0%);

    .submit {
        padding: 20px;
    }

    .input {
        padding: 10px 20px 30px 20px;
        border-bottom: 1px solid #E6E9EA;
    }


    label {
        display: block;
        font-size: 12px;
    }

    input[type=text],
    input[type=email] {
        display: block;
        width: 100%;
        background: #F8FAF9;
        border: 1px solid #E6E9EA;
        border-radius: 8px;
        padding: 4px 10px 4px 15px;
        transition: border-color 0.2s ease-out;
    }

    select {
        display: block;
        width: 100%;
        box-shadow: 0px 0px 1px rgba(0, 0, 0, 0.5), 0px 2px 3px rgba(0, 0, 0, 0.05), 0px 4px 20px rgba(0, 0, 0, 0.04);
        border-radius: 8px;
        padding: 4px 10px 4px 15px;
        background: #FFFFFF url(../../../assets/arrow-dropdown.svg) no-repeat right 10px center;
    }

    button {
        display: block;
        width: 100%;
        color: #FFFFFF;
        background: #141616;
        border-radius: 8px;
        padding: 13px 20px;
        font-weight: 590;
    }

    p {
        position: absolute;
        font-size: 12px;
        transform: translateY(-5px);
        color: red
    }
}

@media(min-width:800px) {
    form {
        width: 400px;
    }
}

@media(min-width:1200px) {
    form {
        transform: translateX(-50%);
    }
}
</style>