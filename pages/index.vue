<template>
    <div class="row justify-content-center">
        <div class="col-lg-6 col-xs-12 mt-3">

            <input class="form-control form-control-lg mb-3" type="text" placeholder="Escribe tu tarea..."
                v-model="tempTask.description" ref="input-temp-task-description" v-on:keyup.enter="saveTask">

            <ul class="list-group" v-if="tasks.length > 0">
                <li class="list-group-item" v-for="(t, i) in tasks">
                    <div class="float-end">
                        <button type="button" class="btn btn-sm" :class="t.done ? 'btn-primary' : 'btn-outline-primary'"
                            v-on:click="doneToggleTask(i)">
                            <i class="bi bi-patch-check"></i>
                        </button>
                        <button type="button" class="btn btn-outline-success btn-sm" v-on:click="editTask(i, $event)"
                            :disabled="t.done">
                            <i class="bi bi-pencil"></i>
                        </button>
                        <button type="button" class="btn btn-outline-danger btn-sm" v-on:click="deleteTask(i)">
                            <i class="bi bi-x-lg"></i>
                        </button>
                    </div>

                    <span :class="{ 'text-decoration-line-through': t.done }">
                        {{ t.description }}
                    </span>
                </li>
            </ul>

            <p class="text-center text-muted" v-else>
                No has escrito ninguna tarea.
            </p>
        </div>
    </div>
</template>

<script>
const defaultTask = {
    description: '',
    done: false,    
}

export default {
    data() {
        return {
            editingTask: false,
            editIndexTask: null,
            tempTask: {
                description: '',
                done: false,
            },
            tasks: [
                {
                    description: 'Una tarea pequeña',
                    done: false,
                },
                {
                    description: 'Hotfix para el tema de token',
                    done: false,
                },
                {
                    description: 'Seeder de la tabla de DynamoDB',
                    done: false,
                },
                {
                    description: 'Migrar servicio de registro',
                    done: false,
                },
                {
                    description: 'Revisar servicio de Geocoding',
                    done: false,
                },
                {
                    description: 'Pendiente meterle EventBridge',
                    done: false,
                }
            ]
        }
    },
    methods: {
        saveTask: function () {
            if (this.editingTask) {
                this.tasks[this.editIndexTask] = this.tempTask

                this.editingTask = false
                this.editIndexTask = null

                this.showMessage('Tarea actualizada.')
            } else {
                this.tasks.push(this.tempTask)
            }

            this.tempTask = defaultTask
        },
        editTask: function (index) {
            this.editingTask = true
            this.editIndexTask = index

            this.tempTask = this.tasks[index]
            this.$refs['input-temp-task-description'].focus()
        },
        doneToggleTask: function (index) {
            this.tasks[index].done = !this.tasks[index].done

            if (this.tasks[index].done) {
                this.showMessage(`La tarea finalizada.`);
            }
        },
        deleteTask: function (index) {
            this.tasks.splice(index, 1)

            this.showMessage(`La tarea eliminada.`);
        },
        // UI methods
        showMessage: function (message) {
            Toastify({
                text: message,
                duration: 3000,
                newWindow: true,
                close: true,
                gravity: "top", // `top` or `bottom`
                position: "right", // `left`, `center` or `right`
                style: {
                    background: "linear-gradient(to right, #00b09b, #96c93d)",
                }
            }).showToast();
        }
    }
}
</script>
