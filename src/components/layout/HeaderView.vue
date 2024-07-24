<template>
    <header class="header">
        <div class="header__content">
            <router-link 
                to="/"       
                class="logo"
            >
                <svg-icon 
                    class="logo__icon"
                    icon="logoPlaceholder"
                    width="24"
                    height="24"
                />
                <div class="logo__name">Логотип</div>
            </router-link>
            <button-custom>Каталог</button-custom>
            <input-custom 
                v-model="searchValue"
                class="product-search"
                inputType="search"
                placeholder="Поиск по 100000 товаров"
            />
            <div class="nav">
                <router-link 
                    to="/"
                    class="nav__item"
                >
                    Информация о компании
                </router-link>
                <router-link 
                    to="/"
                    class="nav__item"
                >
                    Контакты
                </router-link>
                <router-link 
                    to="/"      
                    class="nav__item"
                >
                    Полезные ссылки
                </router-link>
            </div>
        </div>
        <div class="header__mobile-content">
            <svg-icon 
                class="back"
                icon="backArrow"
                width="20"
                height="20" 
            />
            <div class="request">
                <input-custom 
                    id="search-input"
                    v-model="searchValue"
                    class="request__field"
                    placeholder="Запрос"
                    inputType="no-border"
                />
                <div 
                    class="request__subtract"
                >
                    <svg-icon 
                        icon="subtract"
                        width="20"
                        height="20" 
                    />
                </div>
                <button-custom bForm="search">Поиск</button-custom>
            </div>
        </div>
    </header>
</template>

<script>
import ButtonCustom from '../controls/ButtonCustom.vue'
import InputCustom from '../controls/InputCustom.vue'
import SvgIcon from '../controls/SvgIcon.vue'


export default {
    components: {
        SvgIcon,
        ButtonCustom,
        InputCustom
    },
    data() {
        return {
            searchValue: ''
        }
    } 
}
</script>

<style lang="scss" scoped>
    .header {
        font-family: var(--font-family-second);
        margin-bottom: 24px;
        width: 100%;
        &__content {
            display: flex;
            align-items: center;
            .logo {
                padding: 15px 27px;
                width: 145px;
                height: 48px;
                margin-right: 8px;
                display: flex;
                align-items: center;
                gap: 11px;
                font-size: 16px;
            }
            .product-search {
                margin-left: 24px;
                max-width: 1015px;
                width: 100%;
                &::before {
                    z-index: 2;
                    content: '';
                    position: absolute;
                    top: 50%;
                    left: 16px;
                    transform: translateY(-50%);
                    width: 24px;
                    height: 24px;
                    background-image: url('/src/assets/svg/searchItem.svg');
                    background-size: cover;
                    background-repeat: no-repeat;
                }
            }
            .nav {
                margin-left: 24px;
                min-width: 400px;
                text-align: right;
                display: flex;
                align-items: center;
                gap: 20px;
                &__item {
                    &:hover {
                        text-decoration: underline;
                    }
                }
            }
        }
        &__mobile-content {
            display: none;
        }
    }
@media (max-width: 1200px) {
    .header {
      &__content {
        display: none;
      }
      &__mobile-content {
        display: flex;
        gap: 16px;
        .back {
            padding-top: 9.5px;
        }
        .request {
            padding-bottom: 6px;
            width: 100%;
            display: flex;
            align-items: center;
            border-bottom: 1px solid #d5d5d5;
            &__field {
                width: 100%;
            }
            &__subtract {
                margin-left: 18px;
                margin-right: 18px;
            }
        }
      }
    }
}
</style>