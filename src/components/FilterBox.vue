<template>
    <div class="filter">
        <div class="filter__categories">
            <div 
                v-for="(category, index) in categories" 
                :key="category.id" 
                :class="['category', { 'category_active': activeCategoryIndex === index }]" 
                @click="setActiveCategory(index)"
            >
                <div class="category__name">{{ category.name }}</div>
                <div class="category__count">{{ category.count }}</div>
            </div>
        </div>
        <div class="filter__price">
            <div class="header">Цена</div>
            <div class="value">
                <input-custom 
                    inputType="price"
                    type="number"
                    :min="0"
                    :maxlength="6"
                    :step="1"
                    class="value__from" 
                /> 
                <svg-icon 
                    icon="divider"
                    width="10"
                    height="1"
                /> 
                <input-custom 
                    inputType="price"
                    type="number"
                    class="value__to"
                    :min="0"
                    :maxlength="6"
                    :step="1"
                />
            </div>
        </div>
        <div class="filter__section">
            <div class="header header_brand">
                <div class="name">
                    Бренд
                </div>
                <div 
                    class="clear"
                    @click="clearAllBrands"
                >
                    Очистить
                </div>
            </div>
            <input-custom 
                inputType="brand"
                class="search"
                placeholder="Поиск"
            />
            <div class="attributes">
                <div 
                    v-for="(attribute, index) in brandAttributes" 
                    :key="attribute.id" 
                    class="attributes__item"
                >
                    <checkbox-custom 
                        :id="`brand-${attribute.id}`"
                        :value="attribute.checked"
                        @click="useBrand(index)"
                    >
                        {{ attribute.name }}
                    </checkbox-custom>
                    <div class="count">{{ attribute.count }}</div>
                </div>
            </div>
        </div>
        <div class="filter__section">
            <div class="header">Размер</div>
            <div class="attributes">
                <div 
                    v-for="attribute in sizeAttributes" 
                    :key="attribute.id" 
                    class="attributes__item"
                >
                    <checkbox-custom 
                        :id="`size-${attribute.id}`"
                        :value="attribute.checked"
                    >
                        {{ attribute.name }}
                    </checkbox-custom>
                    <div class="count">{{ attribute.count }}</div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import InputCustom from './controls/InputCustom.vue'
import CheckboxCustom from './controls/CheckboxCustom.vue'
import SvgIcon from './controls/SvgIcon.vue'
    export default {
        components: { InputCustom, CheckboxCustom, SvgIcon },
        data() {
            return {
                checked: false,
                categories: [
                    { id: 1, name: 'Название категории 1', count: 2 },
                    { id: 2, name: 'Название категории 2', count: 3 },
                    { id: 3, name: 'Название категории 3', count: 4 },
                    { id: 4, name: 'Название категории 4', count: 5 }
                ],
                brandAttributes: [
                    { id: 1, name: 'Атрибут 1', count: 3, checked: false },
                    { id: 2, name: 'Атрибут 2', count: 4, checked: false },
                    { id: 3, name: 'Атрибут 3', count: 3, checked: false },
                    { id: 4, name: 'Атрибут 4', count: 6, checked: false },
                    { id: 5, name: 'Атрибут 5', count: 3, checked: false },
                    { id: 6, name: 'Атрибут 6', count: 8, checked: false },
                    { id: 7, name: 'Атрибут 7', count: 3, checked: false },
                    { id: 8, name: 'Атрибут 8', count: 1, checked: false },
                    { id: 9, name: 'Атрибут 9', count: 3, checked: false }
                ],
                sizeAttributes: [
                    { id: 1, name: 'Атрибут 1', count: 1, checked: false },
                    { id: 2, name: 'Атрибут 2', count: 3, checked: false },
                    { id: 3, name: 'Атрибут 3', count: 5, checked: false },
                    { id: 4, name: 'Атрибут 4', count: 3, checked: false },
                    { id: 5, name: 'Атрибут 5', count: 2, checked: false },
                    { id: 6, name: 'Атрибут 6', count: 3, checked: false }
                ],
                activeCategoryIndex: 0
            }
        },
        methods: {
            setActiveCategory(index) {
                this.activeCategoryIndex = index;
            },
            useBrand(index) {
                this.brandAttributes[index].checked = !this.brandAttributes[index].checked
            },
            clearAllBrands() {
                for (let attribute of this.brandAttributes) {
                    attribute.checked = false
                }
            }
        },
    }
</script>

<style lang="scss" scoped>
    .filter {
        display: flex;
        flex-direction: column;
        gap: 28px;
        width: 280px;
        &__categories {
            .category {
                cursor: pointer;
                transition: 0.3s;
                display: flex;
                align-items: center;
                justify-content: space-between;
                padding: 7px 16px 7px 32px;
                &__count {
                    font-size: var(--font-size-xs);
                    line-height: 117%;
                    text-align: right;
                    color: var(--text-color-placeholder);
                }
                &_active {
                    padding-left: 8px;
                    .category {
                        &__count {
                            color: var(--text-color);
                        }
                    }
                }
                &:hover {
                    background: #e2efff;
                    border-radius: 5px;
                    .category {
                        &__count {
                            color: var(--text-color);
                        }
                    }
                }
            }
        }
        &__price {
            .header {
                margin-bottom: 16px;
                text-align: center;
                font-weight: 700;
                font-size: 16px;
                line-height: 125%;
            }
            .value {
                display: flex;
                align-items: center;
                gap: 16px;
                &__from {
                    width: 119px;
                    &::before {
                        z-index: 2;
                        content: 'от';
                        position: absolute;
                        top: 11px;
                        left: 8px;
                        width: 12px;
                        height: 14px;
                        font-size: var(--font-size-xs);
                        line-height: 117%;
                        color: var(--text-color-placeholder);
                    }
                }
                &__to {
                    width: 119px;
                    &::before {
                        z-index: 2;
                        content: 'до';
                        position: absolute;
                        top: 11px;
                        left: 8px;
                        width: 12px;
                        height: 14px;
                        font-size: var(--font-size-xs);
                        line-height: 117%;
                        color: var(--text-color-placeholder);
                    }
                }
            }
        }
        &__section {
            .header {
                margin-bottom: 16px;
                text-align: center;
                font-weight: 700;
                font-size: 16px;
                line-height: 125%;
                &_brand {
                    display: flex;
                    align-items: center;
                    justify-content: space-between;
                    margin-bottom: 16px;
                    .name {
                        font-weight: 700;
                        font-size: 16px;
                        line-height: 125%;
                    }
                    .clear {
                        cursor: pointer;
                        font-size: var(--font-size-xs);
                        line-height: 100%;
                        text-decoration: underline;
                        text-decoration-skip-ink: none;
                        text-align: right;
                        color: var(--text-color-placeholder);
                    }
                }
            }
            .search {
                margin-bottom: 16px;
                &::before {
                    z-index: 2;
                    content: '';
                    position: absolute;
                    top: 50%;
                    left: 12px;
                    transform: translateY(-50%);
                    width: 16px;
                    height: 16px;
                    background-image: url('/src/assets/svg/searchBrand.svg');
                    background-size: cover;
                    background-repeat: no-repeat;
                }
            }
            .attributes {
                display: flex;
                flex-direction: column;
                gap: 12px;
                max-height: 180px;
                overflow: auto;
                &__item {
                    padding-right: 13px;
                    display: flex;
                    align-items: center;
                    justify-content: space-between;
                    .count {
                        font-size: var(--font-size-xs);
                        line-height: 117%;
                        text-align: right;
                        color: var(--text-color-placeholder);
                    }
                }
                &::-webkit-scrollbar {
                    width: 3px;
                }
            }
        }
    }
</style>