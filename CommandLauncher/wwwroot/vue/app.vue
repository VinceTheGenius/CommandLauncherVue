Vue.createApp({
        data() {
            return {
                selectedCommand: null,
                commandArea: '',
                commands: [],
                isLoading: false,
                isLoaded: false,
            }
        },
        methods: {
            clickCommand: function () {
                this.isLoading = true;
                axios
                    .get('/Home/Launch', {
                        params: {
                            'Command': this.selectedCommand
                        }
                    })
                    .then(response => {
                        this.isLoading = false;
                        (this.commandArea += response.output);
                    });
            },
            getCommands: function () {
                axios
                    .get('/Home/ListCommand')
                    .then(response => {
                        (this.commands = response);
                        setTimeout(() => { this.isLoaded = true; }, 1000);

                    });
            },
            refresh: function () {
                this.commandArea = '';
            }
        }
    }).mount('#app')