<template>
    <div v-show="!store.isLogIn">
        <h1>회원가입</h1>
        <form @submit.prevent="signUp">
            <label for="profile_image">프로필 이미지</label><br>
            <input type="file" id="profile_image" @change="handleFileChange"><br>
            
            <label for="username">아이디</label><br>
            <input type="text" id="username" v-model.trim="username"><br>

            <label for="password1">비밀번호</label><br>
            <input type="password" id="password1" v-model.trim="password1"><br>

            <label for="password2">비밀번호 확인</label><br>
            <input type="password" id="password2" v-model.trim="password2"><br>

            <label for="nickname">닉네임</label><br>
            <input type="text" id="nickname" v-model.trim="nickname"><br>

            <label for="role">역할</label><br>
            <select id="role" v-model="role">
                <option value="미정">미정</option>
                <option value="감독">감독</option>
                <option value="배우">배우</option>
                <option value="스탭">스탭</option>
            </select><br>

            <input type="text" id="email" placeholder="이메일" v-model="email"><br>

            <input type="text" id="instagram" placeholder="인스타그램" v-model="instagram"><br>

            <input type="text" id="etc" placeholder="기타" v-model="etc"><br>

            <label for="introduction">자기소개</label><br>
            <input type="textarea" id="introduction" v-model="introduction"><br>

            <button>회원가입</button>
        </form>
    </div>
    <div v-show="store.isLogIn">
        <SignUpComplete />
    </div>
</template>

<script setup>
import { ref } from 'vue'
import { useAccountStore } from '@/stores/account'
import SignUpComplete from '@/components/SignUpComplete.vue'

const store = useAccountStore()

const profile_image = ref(null)
const username = ref(null)
const password1 = ref(null)
const password2 = ref(null)
const nickname = ref(null)
const role = ref(null)
const email = ref(null)
const instagram = ref('')
const etc = ref('')
const introduction = ref('')

const handleFileChange = (event) => {
    if (event.target.files.length > 0) {
        profile_image.value = event.target.files[0] // 선택한 파일을 설정
    } else {
        profile_image.value = null // 파일이 없으면 null로 초기화
    }
}

const signUp = function () {
    const formData = new FormData()
    if (profile_image.value) {
        formData.append('profile_image', profile_image.value)
    }
    formData.append('username', username.value)
    formData.append('password1', password1.value)
    formData.append('password2', password2.value)
    formData.append('nickname', nickname.value)
    formData.append('role', role.value)
    formData.append('email', email.value)
    formData.append('instagram', instagram.value)
    formData.append('etc', etc.value)
    formData.append('introduction', introduction.value)
    store.signUp(formData)
}
</script>

<style scoped>

</style>