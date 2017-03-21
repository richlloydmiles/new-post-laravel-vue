<template>
  <div class="row">
    <div class="col-md-8 col-md-offset-2">
      <div class="panel panel-default">
        <div class="panel-heading"> New Post</div>
        <form method="POST" action="/projects" @submit.prevent="onSubmit" @keydown="form.errors.clear($event.target.name)">

          <div class="panel-body">
            <div class="form-group">
              <label for="title">Title:</label>
              <input v-model="form.title" type="text" class="form-control" id="title">
              <span class="help is-danger" v-if="form.errors.has('title')" v-text="form.errors.get('title')"></span>
            </div>

            <div class="form-group">
              <label for="body">Body:</label>
              <textarea v-model="form.body" cols="30" rows="10" id="body" class="form-control"></textarea>
              <span class="help is-danger" v-if="form.errors.has('body')" v-text="form.errors.get('body')"></span>
            </div>
          </div>
          <div class="control">
            <button class="button is-primary" :disabled="form.errors.any()">Create</button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>

/****  in controller *****

/*    public function store(Request $request)
    {
      $this->validate(request(), [
        'title' => 'required',
        "body" => 'required'
        ]);
      Post::forceCreate([
        'title' => request('title'),
        'body' => request('body'),
        ]);
      return ['message' => 'Post Created!'];
  }

  */

 //https://github.com/richlloydmiles/form-errors-vue

  import Form from '../lib/form'

  export default {
    data() {
      return {
        form: new Form({
          title: '',
          body: ''
        })
      }
    },
    methods: {
      onSubmit() {
        this.form.post('/posts')
        .then(response => alert('Wahoo!'));
      }
    }
  }
</script>
