<template>
  <main>
    <!-- Кнопка -->
    <button
      type="button"
      class="btn btn-primary"
      data-bs-toggle="modal"
      data-bs-target="#myModal"
    >
      Открыть модальное окно
    </button>

    <!-- Модальное окно -->
    <div
      class="modal fade"
      id="myModal"
      aria-labelledby="exampleModalLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLabel">Заголовок</h5>
            <button
              type="button"
              class="close"
              data-bs-dismiss="modal"
              aria-label="Close"
            >
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="modal-body">
            <!-- Список -->
            <select
              class="form-select"
              id="mySelect2"
              style="width: 100%"
            ></select>
          </div>
          <div class="modal-footer">
            <button
              type="button"
              class="btn btn-secondary"
              data-bs-dismiss="modal"
            >
              Закрыть
            </button>
            <button type="button" class="btn btn-primary">Ок</button>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  setup() {
    $(document).ready(function () {
      $("#mySelect2").select2({
        ajax: {
          url: "https://gorest.co.in/public/v2/users",
          dataType: "json",
          delay: 500,
          cache: true,
          data: function (params) {
            let query = {
              q: params.term,
            };
            return query;
          },
          processResults: function (data) {
            return {
              results: data,
            };
          },
        },
        templateResult: function (repo) {
          if (repo.id) {
            return repo.id + " : " + repo.name;
          }
        },
        templateSelection: function (repo) {
          if (repo.id) {
            return repo.id + " : " + repo.name;
          }
        },
      });
    });
  },
};
</script>

<style>
.select2-close-mask {
  z-index: 2099;
}
.select2-dropdown {
  z-index: 3051;
}
</style>
