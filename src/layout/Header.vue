<template>
    <header>
        <div class="header__content">
            <div class="header__logo">
                <img alt="Logo" 
                    src="@/assets/images/logo.png" 
                    class="header__logo_ellipse"
                />
                <img alt="Logo" 
                    class="header__logo_space" 
                    src="@/assets/images/Space.png" 
                />
            </div>
            <div class="header__contacts">
                <a class="header__contacts_phone" 
                    href="tel:+88000000000">
                    800 000 00 00
                </a>
                <a class="header__contacts_email" 
                    href="mailto:sales@logo.ru">
                    sales@logo.ru
                </a>
            </div>
            <div class="header__contacts_mobile">
                <a href="tel:+88000000000">
                    <img alt="phone" src="@/assets/images/phone.png" 
                        class="header__contacts_phone-mobile"/>
                </a>
                <a href="mailto:sales@logo.ru">
                    <img alt="mail" src="@/assets/images/mail.png" 
                        class="header__contacts_email-mobile" />
                </a>
            </div>  
        </div>
        
  </header>
</template>

<style lang="scss" scoped>
header {
    display: flex;
    align-items: center;
    width: 100%;
    height: 88px;
    position: fixed;
    background-color: white;
    z-index: 2;

    @media(max-width: $breakpoint_tablet) {
        height: 56px;
    }
}

.header__content {
    width: $content-width;
    margin: auto;
    display: flex;
    justify-content: space-between;
}

.header__logo {
    display: flex;
    align-items: center;
    cursor: pointer; 
}

.header__logo_ellipse {
    @media(max-width: $breakpoint_tablet) {
        height: 24px;
        width: 24px;
    }
}
.header__logo_space {
    margin-left: 15px;

    @media(max-width: $breakpoint_tablet) {
        width: 62px;
        height: 17px;
    }
}

.header__contacts {
    font-size: $header__contacts_text-size;
    font-weight: $header__contacts_text-weight;

    @media(max-width: $breakpoint_tablet) {
        display: none;
    }
}

.header__contacts_mobile {
    display: flex;
    align-items: center;

    @media(min-width: $breakpoint_tablet) {
        display: none;
    }
}

.header__contacts_phone-mobile {
    margin-right: 20px;
}

.header__contacts_email {
    margin-left: 20px;
    text-decoration: none;
    color: $header__contacts_text-color;
}

.header__contacts_phone {
    text-decoration: none;
    color: $header__contacts_text-color;
}
</style>