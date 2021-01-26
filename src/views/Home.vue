<template>
  <div class="home">
    <editor id="tinymce" v-model="tinymceHtml" :init="init"></editor>
    <div v-html="tinymceHtml"></div>
  </div>
</template>

<script>
// @ is an alias to /src
import tinymce from 'tinymce/tinymce';
import 'tinymce/themes/modern/theme';
import Editor from '@tinymce/tinymce-vue';
import 'tinymce/plugins/image';
import 'tinymce/plugins/link';
import 'tinymce/plugins/code';
import 'tinymce/plugins/table';
import 'tinymce/plugins/lists';
import 'tinymce/plugins/contextmenu';
import 'tinymce/plugins/wordcount';
import 'tinymce/plugins/colorpicker';
import 'tinymce/plugins/textcolor';
import 'tinymce/plugins/fullscreen';
export default {
  name: 'Home',
  data() {
    return {
      tinymceHtml: '请输入内容',
      init: {
        selector: '#tinymce', //tinymce的id
        language_url: '/tinymce/lang/zh_CN.js',
        language: 'zh_CN',
        skin_url: '/tinymce/skins/lightgray',
        width: 600,
        height: 300,
        automatic_uploads: false,
        images_upload_url: '/upload',
        file_browser_callback_types: 'image video',
        plugins: 'link lists image code table colorpicker textcolor wordcount contextmenu fullscreen',
        toolbar:
          'bold italic underline strikethrough | fontsizeselect | forecolor backcolor | alignleft aligncenter alignright alignjustify | bullist numlist | outdent indent blockquote | undo redo | link unlink image code | removeformat | fullscreen',
        branding: false,
        images_upload_handler: function(blobInfo, success, failure) {
          let formData = new FormData();
          formData.append('file', blobInfo.blob(), blobInfo.filename());
          console.log('formData', blobInfo);
        },
      },
    };
  },
  components: {
    Editor,
  },
  mounted() {
    tinymce.init({});
    this.time();
  },
  methods: {
    time() {
      setTimeout(() => {
        console.log(this.tinymceHtml);
        this.time();
      }, 2000);
    },
  },
};
</script>
