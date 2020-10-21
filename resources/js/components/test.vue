<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-12">
                <div class="card">
                    <LocaleDropdown></LocaleDropdown>
                    <div class="card-header">
                        {{ $t('products.table.products') }}
                        <button class="btn btn-sm btn-success float-right">
                            {{ $t('products.table.buttons.new') }}
                        </button>
                    </div>

                    <div class="card-body">
                        <table class="table table-hover">
                            <thead>
                            <tr>
                                <th scope="col">{{ $t('products.table.name') }}</th>
                                <th scope="col">{{ $t('products.table.description') }}</th>
                                <th scope="col">{{ $t('products.table.quantity') }}</th>
                                <th scope="col">{{ $t('products.table.price') }}</th>
                                <th scope="col">{{ $t('products.table.actions') }}</th>
                            </tr>
                            </thead>
                            <tbody>
                            <tr v-for="(product, index) in products" :key="product.id">
                                <td>{{ translate(product.name) }}</td>
                                <td>{{ translate(product.description) }}</td>
                                <td>{{ product.quantity }}</td>
                                <td>{{ product.price }}</td>
                                <td>
                                    <div class="btn-group" role="group" aria-label="Tag Action Buttons">
                                        <button  class="btn btn-sm btn-primary mr-1">
                                            <i class="fas fa-pencil-alt mr-1"></i>
                                            {{ $t('products.table.buttons.edit') }}
                                        </button>
                                        <button class="btn btn-sm btn-danger">
                                            <i class="fas fa-trash mr-1"></i>
                                            {{ $t('products.table.buttons.delete') }}
                                        </button>
                                    </div>
                                </td>
                            </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import LocaleDropdown from "../Helpers/LocaleDropdown";

    export default {
        name: "ProductComponent",
        props: {
            products: {
                type: Array,
                default: () => {
                    return []
                }
            }
        },
        components: {
            LocaleDropdown
        },
        methods: {
            translate(name) {
                try {
                    JSON.parse(name);
                } catch (e) {
                    return name;
                }
                let translated = JSON.parse(name);
                return translated[this.$i18n.locale]
            },
        }
    }
</script>