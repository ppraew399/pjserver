<template>
    <div>
        <main-header navsel="back"></main-header>
        <br><br><br>
        <center><h1>แก้ไขรายละเอียด ผู้ใช้งาน</h1><br>
        <form v-on:submit.prevent = "editUser">
            <table border="0">
            <tr>
                <th class="d">
                    <center><b>name:</b></center>
                </th>
                <th class ="c">
                    <input class="form-control center_div" type="text" v-model="user.name">
                </th>
            </tr>
            <br>
            <tr>
                <th class="d">
                    <center><b>lastname:</b></center>
                </th>
                <th class ="c">
                    <input class="form-control center_div" type="text" v-model="user.lastname">
                </th>
            </tr>
            <br>
            <tr>
                <th class="d">
                    <center><b>email:</b></center>
                </th>
                <th class ="c">
                    <input class="form-control center_div" type="text" v-model="user.email">
                </th>
            </tr>
            <br>
            <tr>
                <th class="d">
                    <center><b>password:</b></center>
                </th>
                <th class ="c">
                    <input class="form-control center_div" type="text" v-model="user.password">
                </th>
            </tr>
            <br>
            <tr>
                <th class="d">
                    <center><b>status:</b></center>
                </th>
                <th class ="c">
                    <input class="form-control center_div" type="text" v-model="user.status">
                </th>
            </tr>
            <br>
            <tr>
                <th class="d">
                    <center><b>type:</b></center>
                </th>
                <th class ="c">
                    <input class="form-control center_div" type="text" v-model="user.type">
                </th>
            </tr>
            </table>
            <br>
                <p>
                    <button class="btn btn-success btn-sm" type="submit">แก้ไข</button>
                    <button class="btn btn-sm secondary" v-on:click="navigateTo('/users')">ย้อนกลับ</button>
                </p>
            
        </form>
        
            
        
        
    </center>
    </div>
</template>
<script>
    import UsersService from '@/services/UsersService'
    export default {
        data () {
            return {
                user: {
                name: '',
                lastname: '',
                email: '',
                password: '',
                status: 'active'
            }
        }
        },
        methods: {
            async editUser () {
                try {
                    await UsersService.put(this.user)
                    this.$router.push({
                    name: 'users'
                })
                } catch (err) {
                    console.log(err)
                }
            },
            navigateTo (route) {
                this.$router.push(route)
            },
        },
        async created () {
            try {
                let userId = this.$route.params.userId
                this.user = (await UsersService.show(userId)).data
            } catch (error) {
                console.log (error)
            }
        }
    }
</script>
<style scoped>
    .center_div {
        width:100%;
    }
    .c {
        width: 600px ;
    }
    .d{
        width: 100px ;
    }
</style>