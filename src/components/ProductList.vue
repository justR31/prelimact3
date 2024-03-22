<template>
    <div class="product-list">
        <table>
            <tr>
                <th><h1>Product List</h1></th>
            </tr>
            <tr>
                <th>
                    Product Name
                </th>
                <th>
                    Product Price
                </th>
            </tr>
            <tr>
                <td>Celeteque Face Wash</td>
                <td>₱ 230.00</td>
            </tr>
            <tr>
                <td>Celeteque Moisturizer</td>
                <td>₱ 250.00</td>
            </tr>
            <tr>
                <td>Colgate Toothbrush</td>
                <td>₱ 85.00</td>
            </tr>
            <tr>
                <td>Beard Trimmer</td>
                <td>₱ 2,900.00</td>
            </tr>
            <tr>
                <td>Lip Balm</td>
                <td>₱ 50.00</td>
            </tr>
            <tr>
                <td>Oxygn Cologne</td>
                <td>₱ 480.00</td>
            </tr>
            <tr>
                <td>BVLGARI Ocean Series</td>
                <td>₱ 4799.00</td>
            </tr>
            <tr>
                <td>Dove Men + Care Body Wash</td>
                <td>₱ 230.00</td>
            </tr>
            <tr>
                <td>Metal Tongue Scraper</td>
                <td>₱ 50.00</td>
            </tr>
            <tr>
                <td>Paper Stem Cotton Buds</td>
                <td>₱ 48.00</td>
            </tr>
        </table>
        <ItemList :items="items" @add-item="addItem" />
        <ShoppingCart :cart="cart" @remove-item="removeItem" @toggle-editing="toggleEditing"
            @update-quantity="updateQuantity" />
        <p class="total">Total of items: ₱{{ calculateTotal() }}</p>
    </div>
</template>

<script>
import ItemList from './ItemList.vue';
import ShoppingCart from './ShoppingCart.vue';

export default {
    components: {
        ItemList,
        ShoppingCart,
    },
    data() {
        return {
            items: [
                { name: 'Celeteque Face Wash', cost: 230 },
                { name: 'Celeteque Moisturizer', cost: 250 },
                { name: 'Colgate Toothbrush', cost: 85 },
                { name: 'Beard Trimmer', cost: 2900 },
                { name: 'Lip Balm', cost: 50 },
                { name: 'Oxygn Cologne', cost: 480 },
                { name: 'BVLGARI Ocean Series', cost: 4799 },
                { name: 'Dove Men + Care Body Wash', cost: 230 },
                { name: 'Metal Tongue Scraper', cost: 50 },
                { name: 'Paper Stem Cotton Buds', cost: 48 }
            ],
            cart: []
        };
    },
    methods: {
        addItem(item) {
            this.cart.push(item);
        },
        removeItem(index) {
            this.cart.splice(index, 1);
        },
        calculateTotal() {
            return this.totalPrice;
        },
        toggleEditing(index) {
            this.cart[index].editable = true;
            this.cart[index].newQuantity = this.cart[index].quantity;
        },
        updateQuantity(payload) {
            const { index, newQuantity } = payload;
            if (newQuantity <= 0) {
                alert('Invalid Quantity');
                return;
            }
            this.cart[index].quantity = newQuantity;
            this.cart[index].editable = false;
        }
    },
    computed: {
        totalPrice() {
            return this.cart.reduce((total, item) => total + (item.cost * item.quantity), 0);
        }
    },
};
</script>