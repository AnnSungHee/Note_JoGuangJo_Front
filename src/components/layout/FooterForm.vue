<template>
    <v-footer padless class="justify-center pl-0">
        <v-card flat class="text-center" width="100%">
            <v-divider></v-divider>
            <div align="center">
                <v-btn v-for="icon in icons" :key="icon" :to="getLink(icon)" class="mx-1 icon-btn" icon>
                    <v-icon size="24px">
                        {{ icon }} 
                    </v-icon>
                </v-btn>
            </div>
            <v-card-text class="pt-4">
                서울특별시 강남구 테헤란로14길 6 남도빌딩 KH정보교육원<br>
                <a v-if="showButton" style="color: grey;" @click="resignhandler" class="custom-link">회원 탈퇴</a><br>
                <strong>ⓒ BOOK_YOU_LOVE</strong>
                {{ new Date().getFullYear() }}
            </v-card-text>
        </v-card>
    </v-footer>
</template>

<script>
export default {
    name: "FooterForm",
    data: () => ({
        icons: [
            "mdi-instagram",
            "mdi-youtube",
            "mdi-facebook"
            ],
        links: {
        "mdi-instagram": "/instagram",
        "mdi-youtube": "/youtube",
        "mdi-facebook": "/facebook"
        }
    }),
    computed: {
        showButton() {
            return this.$route.path === '/mypage';
        }
    },
    methods: {
        getLink(icon) {
            return this.links[icon];
        },
        async resignhandler() {
            const result = await this.$store.dispatch("account/resign");
            if (result) {
                if (this.$route.path !== "/") {
                    this.$router.push("/");
                }
            } else {
                alert("회원탈퇴중에 오류가 발생했습니다.")
            }
        },
    }
}
</script>

<style scoped>
    a.custom-link {
        text-decoration: none;
    }

    .hidden {
        visibility: hidden;
    }

    .icon-btn:hover {
        background-color: rgba(255, 242, 189, 0.5);
        color: #FFC107 !important;
    }
</style>
