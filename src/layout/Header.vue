<template>
    <header>
        <router-link 
            class="header__logo"
            :to="Space"
        >
            <img alt="Logo" src="@/assets/images/logo.png" />
            <img alt="Logo" class="header__logo_space" src="@/assets/images/Space.png" />
        </router-link>
        <div class="header__contacts">
            <a class="header__contacts_phone" href="tel:+88000000000">8 800 000 00 00</a>
            <a class="header__contacts_email" href="mailto:sales@logo.ru">sales@logo.ru</a>
        </div>
  </header>
</template>

<style lang="scss" scoped>
header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    width: 90vw;
    margin: auto;
    height: 88px;
}

.header__logo {
    display: flex;
    align-items: center;
    cursor: pointer;
}
.header__logo_space {
    margin-left: 15px;
}

.header__contacts {
    font-size: $header__contacts_text-size;
    font-weight: $header__contacts_text-weight;
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