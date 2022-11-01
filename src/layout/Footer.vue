<template>
    <footer>
        <div class="footer__content">
            <router-link 
                :to="Space"
                class="footer__content_logo"
            >
                <img alt="Logo" src="@/assets/images/logo-footer.png" class="footer__content_logo-ellipse" />
                <img alt="Logo" class="footer__content_logo-space" src="@/assets/images/Space-footer.png" />
            </router-link>
            <div class="footer__content_nav">
                <span class="footer__content_nav-item">Готовые решения</span>
                <span class="footer__content_nav-item">О нас</span>
                <span class="footer__content_nav-item">Блог</span>
                <span class="footer__content_nav-item">Контакты</span>
            </div>
        </div>
        <div class="footer__contacts">
            <span class="footer__contacts_copyright">
                © ООО «Лого», 2008—2022
            </span>
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
    //height: 228px;
    background-color: $footer__background-color;
    color: $footer__text-color;

    @media(max-width: $breakpoint_tablet) {
        //height: 252px;
    }
}

.footer__content_nav {
    font-weight: $footer__content_text-weight;
    font-size: $footer__content_text-size;
    line-height: $footer__content_line-height;

    @media(max-width: $breakpoint_tablet) {
        width: 50%;
        display: flex;
        flex-wrap: wrap;
        margin-top: 5px;
        font-size: $footer__content_text-size-mobile;
        line-height: $footer__content_line-height-mobile;
    }

    @media(max-width: $breakpoint_mobile) {
        width: 90%;
    }
}

 .footer__content_nav-item {
    margin-left: 50px;
    cursor: pointer;

    @media(max-width: $breakpoint_tablet) {
        margin-left: 0px;
        width: 50%;
        margin-top: 20px;
    }

}

.footer__contacts_links {
    @media(max-width: $breakpoint_tablet) {
        order: 1;
    }
}

.footer__contacts_copyright {
    line-height: $footer__contacts_copyright-line-height;

    @media(max-width: $breakpoint_tablet) {
        order: 2;
        line-height: $footer__contacts_copyright-line-height-mobile;
        font-size: $footer__contacts_copyright-text-size-mobile;
    }
}

.footer__content {
    display: flex;
    justify-content: space-between;
    width: $content-width;
    margin: auto;
    padding-top: 50px;

    @media(max-width: $breakpoint_tablet) {
        flex-direction: column;
        padding-top: 23px;
    }
}

.footer__contacts {
    display: flex;
    justify-content: space-between;
    width: $content-width;
    margin: auto;
    margin-top: 65px;
    padding-bottom: 50px;

    @media(max-width: $breakpoint_tablet) {
        flex-direction: column;
        margin-top: 35px;
        padding-bottom: 22px;
    }
}

.footer_contacts_link-item {
    margin-left: 20px;
    cursor: pointer;

    @media(max-width: $breakpoint_tablet) {
        margin-left: 0px;
        margin-right: 20px;
        margin-bottom: 22px;
    }
}

.footer__content_logo-space {
    margin-left: 20px;

    @media(max-width: $breakpoint_tablet) {
        width: 83px;
        height: 22px;
        margin-left: 15px;
    }
}

.footer__content_logo {
    cursor: pointer;
}

.footer__content_logo-ellipse {
    @media(max-width: $breakpoint_tablet) {
        width: 32px;
        height: 32px;
    }
}
</style>