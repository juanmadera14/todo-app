<template>
    <div id="app_login" class="container">

        <div class="row justify-content-center">
            <div class="col-5 mt-3">
                <h3 class="text-center">
                    Iniciar Sesión
                </h3>

                <form action="#" v-on:submit.prevent="login" autocomplete="off">

                    <div class="mb-3">
                        <label for="email" class="form-label">Correo Electrónico</label>
                        <input type="email" id="email" placeholder="Ingrese su correo electrónico" v-model="email"
                            class="form-control">
                    </div>

                    <div class="mb-3">
                        <label for="password" class="form-label">Contraseña</label>
                        <input type="password" id="password" ref="password" placeholder="Ingrese contraseña"
                            v-model="password" class="form-control">
                    </div>

                    <div class="text-center">
                        <button type="submit" class="btn btn-primary">
                            Iniciar Sesión
                        </button>
                    </div>
                </form>

            </div>
        </div>
    </div>
</template>
  
<script>
export default {
    layout: 'default',
    data: {
        email: 'kennitromero@gmail.com',
        password: 'c0d3_c0d3',
    },
    methods: {
        login: function () {
            fetch('http://localhost/api/1.0/todo/users/login', {
                method: 'POST',
                mode: 'no-cors',
                headers: {
                    accept: 'application/json',
                    'content-type': 'application/json'
                },
                body: JSON.stringify({
                    email: this.email,
                    password: this.password
                }),
            }).then(response => response.json())
                .then(data => {
                    console.log(data)
                });
        }
    }
}
</script>