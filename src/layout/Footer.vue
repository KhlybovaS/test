<template>
    <footer>
        <div class="footer__content">
            <router-link 
                :to="Space"
                class="footer__content_logo"
            >
                <img alt="Logo" src="@/assets/images/logo-footer.png" />
                <img alt="Logo" class="footer__logo_space" src="@/assets/images/Space-footer.png" />
            </router-link>
            <div class="footer__content_nav">
                <span class="footer__content_nav-item">Готовые решения</span>
                <span class="footer__content_nav-item">О нас</span>
                <span class="footer__content_nav-item">Блог</span>
                <span class="footer__content_nav-item">Контакты</span>
            </div>
        </div>
        <div class="footer__contacts">
            <span>© ООО «Лого», 2008—2022</span>
            <div class="footer__contacts_links">
                <img alt="Telegram" src="@/assets/images/telegram.png" class="footer_contacts_link-item"/>
                <img alt="VK" src="@/assets/images/vk.png" class="footer_contacts_link-item"/>
                <img alt="Twitter" src="@/assets/images/twitter.png" class="footer_contacts_link-item"/>
                <img alt="Youtube" src="@/assets/images/youtube.png" class="footer_contacts_link-item"/>
            </div>
        </div>
    </footer>
</template>

<style lang="scss" scoped>
footer {
    height: 228px;
    background-color: $footer__background-color;
    color: $footer__text-color;
}

.footer__content_nav {
    font-weight: $footer__content_text-weight;
    font-size: $footer__content_text-size;
    line-height: $footer__content_line-height;
}

 .footer__content_nav-item {
    margin-left: 50px;
    cursor: pointer;
}

.footer__content {
    display: flex;
    justify-content: space-between;
    width: 90vw;
    margin: auto;
    padding-top: 50px;
}

.footer__contacts {
    display: flex;
    justify-content: space-between;
    width: 90vw;
    margin: auto;
    margin-top: 70px;
}

.footer_contacts_link-item {
    margin-left: 20px;
    cursor: pointer;
}

.footer__logo_space {
    margin-left: 20px;
}

.footer__content_logo {
    cursor: pointer;
}
</style>