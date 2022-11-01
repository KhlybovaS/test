<template>
    <div class="promo">
        <img alt="promo-logo" class="promo__logo" src="@/assets/images/K4C_1.png" />
        <div class="promo__content">
            <div class="promo__content_title">
                Как бизнесу сохранять<br/>IT-кадры на фоне кризиса
            </div>
            <div class="promo__content_subtitle">
                Инструменты, которые могут использовать компании<br/>для удержания сотрудников
            </div>
            <div class="promo__content_btn">
                Подробнее
            </div>
            <div class="promo__dots">
                <div class="promo__dots_origin"></div>
                <div class="promo__dots_transparent"></div>
                <div class="promo__dots_transparent"></div>
            </div>
        </div>
    </div>
</template>

<style lang="scss" scoped>
.promo {
    width: 100%;
    height: 546px;
    position: relative;
    background: linear-gradient(45deg, $promo__background-color_begin, $promo__background-color_end);

    @media (max-width: $breakpoint_tablet) {
        height: 365px;
    }
}

.promo__logo {
    position: absolute;
    right: 0;
    z-index: 1;
    bottom: 0;

    @media (max-width: $breakpoint_tablet) {
        height: 265px;
    }

    @media (max-width: $breakpoint_mobile) {
        height: 170px;
    }
}

.promo__content {
    width: $content-width;
    margin: auto;
    padding-top: 100px;
    position: relative;
    z-index: 10;

    @media (max-width: $breakpoint_tablet) {
        padding-top: 25px;
    }
}

.promo__content_title {
    color: $promo__text-color;
    font-size: $promo__text-size;
    line-height: $promo__title_line-height;
    font-weight: $promo__title_text-weight;

    @media (max-width: $breakpoint_tablet) {
        font-size: $promo__text-size-mobile;
        line-height: $promo__title_line-height-mobile;
    }
}

.promo__content_subtitle {
    color: $promo__text-color;
    line-height: $promo__subtitle_line-height;
    font-size: $promo__subtitle_font-size;
    padding-top: 40px;
    padding-bottom: 38px;

    @media (max-width: $breakpoint_tablet) {
        font-size: $promo__subtitle_font-size-mobile;
        line-height: $promo__subtitle_line-height-mobile;
        padding-top: 30px;
        padding-bottom: 30px;
    }
}

.promo__content_btn {
    background-color: $promo__btn-color;
    border-radius: 10px;
    color: $promo__btn_text-color;
    padding: 16px 32px;
    display: inline-block;
    font-size: $promo__btn_text-size;
    line-height: $promo__btn_line-height;
    font-weight: $promo__btn_text-weight;
    cursor: pointer;

    @media (max-width: $breakpoint_tablet) {
        font-size: $promo__btn_text-size-mobile;
        line-height: $promo__btn_line-height-mobile;
        padding: 14px 24px;
    }
}

.promo__dots {
    margin-top: 114px;
    display: flex;

    @media (max-width: $breakpoint_mobile){
        margin-top: 95px;
    }
}

.promo__dots_origin {
    width: 29px;
    height: 3px;
    border-radius: 2px;
    background-color: white;
    margin-right: 6px;

    @media (max-width: $breakpoint_tablet) {
        width: 20px;
    }
}

.promo__dots_transparent {
    width: 29px;
    height: 3px;
    border-radius: 2px;
    background-color: white;
    margin-right: 6px;
    opacity: 30%;

    @media (max-width: $breakpoint_tablet) {
        width: 20px;
    }
}
</style>