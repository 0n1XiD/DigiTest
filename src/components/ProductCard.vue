<template>
    <div class="product-card">
        <div class="product-card__image"
             :class="{'product-card__image_out-stock': !stock}">
            <svg-icon 
                icon="itemPlaceholder"
                width="60"
                height="60"
            />
        </div>
        <div class="product-card__content">
            <div class="brand">{{ brand }}</div>
            <div class="name">{{ name }}</div>
            <div 
                v-if="stock"
                class="price"
            >
                {{ price }} ₽
                <div 
                    v-if="oldPrice" 
                    class="price_old"
                >
                    {{ oldPrice }} ₽
                </div>
            </div>
            <button-custom 
                v-if="stock"
                bForm="buy"
            >
                Купить
            </button-custom>
            <button-custom 
                v-else
                bForm="out-stock"
            >
                Сообщить о поступлении
            </button-custom>
        </div>
        <div 
            v-if="hit"
            class="product-card__hit"
        >
            Хит продаж 
            <svg-icon 
                icon="fire"
                width="20"
                height="20"
            />
        </div>
        <div 
            v-if="discount > 0"      
            class="product-card__discount"
        >
            {{ discount }}%
        </div>
    </div>
</template>

<script>
import ButtonCustom from './controls/ButtonCustom.vue'
import SvgIcon from './controls/SvgIcon.vue'
export default {
    components: { SvgIcon, ButtonCustom },
    props: {
        brand: {
            type: String,
            default: 'Бренд'
        },
        name: {
            type: String,
            default: 'Полное название товара в несколько строк для вида с обрывом в конце и всякими плюшками с чайным сервизом'
        },
        price: {
            type: String,
            default: '5 990'
        },
        oldPrice: {
            type:  String,
            default: null
        },
        hit: {
            type: Boolean,
            default: false
        },
        discount: {
            type: Number,
            default: 0
        },
        stock: {
            type: Boolean,
            default: true,
        }
    }
}
</script>

<style lang="scss" scoped>
    .product-card {
        position: relative;
        &__image {
            transition: 0.3s;
            margin-bottom: 16px;
            height: 200px;
            background: #f8f8fa;
            width: 100%;
            display: flex;
            align-items: center;
            justify-content: center;
            i {
                transition: 0.3s;
            }
            &_out-stock {
                background: #F8F8FA;
                opacity: 0.5;
            }
        }
        &__content {
            .brand {
                margin-bottom: 8px;
                line-height: 114%;
                color: var(--text-color-placeholder);
            }
            .name {
                height: 32px;
                line-height: 114%;
                margin-bottom: 16px;
                line-clamp: 2;
                -webkit-line-clamp: 2;
                display: -webkit-box;
                -webkit-box-orient: vertical;
                overflow: hidden;
            }
            .price {
                gap: 8px;
                display: flex;
                align-items: center;
                font-weight: 700;
                font-size: 16px;
                line-height: 87%;
                color: #333;
                &_old {
                    font-size: var(--font-size-xs);
                    line-height: 117%;
                    text-decoration: line-through;
                    color: var(--text-color-placeholder);
                }
            }
            .button {
                &_buy {
                    margin-top: 16px;
                }
                &_out-stock {
                    margin-top: 46px;
                }
            }
        }
        &__hit {
            position: absolute;
            top: 12px;
            left: 12px;
            display: flex;
            align-items: center;
            gap: 4px;
            background-color: white;
            border: 1px solid #f2f2f2;
            border-radius: 4px;
            padding: 0px 8px;
            height: 32px;
        }
        &__discount {
            position: absolute;
            top: 162px;
            left: 12px;
            font-weight: 700;
            line-height: 100%;
            background: #7397f5;
            border-radius: 4px;
            padding: 6px 10px;
            color: white;
        }
        &:hover {
          .product-card {
            &__image {
                cursor: pointer;
                i {
                    scale: 1.5;
                }
            }
            &__content {
                .name {
                    cursor: pointer;
                    color: #125BAE;
                }
            }
          }  
        }
    }
</style>