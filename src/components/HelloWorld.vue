<template>
    <Page class="page">
        <ActionBar class="action-bar" title="Hello world">
            <NavigationButton text="Go Back" android.systemIcon="ic_menu_back" @tap="$router.push('/home')"/>
        </ActionBar>
        <StackLayout class="form">
            <StackLayout class="input-field">
                <TextField class="input" hint="Pups Name"></TextField>
            </StackLayout>
            <Button text="Select Image" class="btn btn-primary" @tap="selectImage"></Button>
            <Button text="Look for my Pup" class="btn btn-primary"></Button>
        </StackLayout>
    </Page>
</template>

<script>
    let imagepicker = require("nativescript-imagepicker")
    export default {
        data () {
            return {
                surprise: false,
                dogName: '',
                dogLabel: '',
                labelList: []
            };
        },
        methods: {
            addLabel: function () {
                this.labelList.push(this.dogLabel)
                this.dogLabel = ''
                console.log(this.labelList.length)
            },
            selectImage: function () {
                let context = imagepicker.create({
                    mode: "single" // use "multiple" for multiple selection
                })
                context
                    .authorize()
                    .then(function() {
                        return context.present();
                    })
                    .then(function(selection) {
                        selection.forEach(function(selected) {
                            // process the selected image
                            console.log(selected.nativeImage)
                        });
                        list.items = selection;
                    }).catch(function (e) {
                    // process error
                });
            }
        }
    };
</script>

<style scoped>
    .page {
        align-items: center;
        flex-direction: column;
    }
    .form {
        margin-left: 30;
        margin-right: 30;
        flex-grow: 2;
        vertical-align: middle;
    }

    TextField {
        border-width: 0 0 1 0;
        border-bottom-color: black;
    }

</style>
