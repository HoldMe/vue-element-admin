<template>
  <el-form>
    <el-form-item label="Icon">
      <br>
      <el-upload
        action=""
        :on-error="onError"
        :on-preview="onPreview"
        :limit="limit"
        :file-list="fileList"
        list-type="picture-card"
      >
        <div class="avatar-uploader">
          <i class="el-icon-plus avatar-uploader-icon" />
        </div>
      </el-upload>
    </el-form-item>
    <el-form-item label="Name">
      <el-input v-model.trim="user.name" />
    </el-form-item>
    <el-form-item label="Email">
      <el-input v-model.trim="user.email" />
    </el-form-item>
    <el-form-item>
      <el-button type="primary" @click="submit">Update</el-button>
    </el-form-item>
  </el-form>
</template>

<script>
export default {
  props: {
    user: {
      type: Object,
      default: () => {
        return {
          name: '',
          email: ''
        }
      }
    },
    limit: {
      type: Number,
      default: 1
    }
  },
  data() {
    return {
      fileList: [],
      iconPlusVisible: true
    }
  },
  methods: {
    submit() {
      this.$message({
        message: 'User information has been updated successfully',
        type: 'success',
        duration: 5 * 1000
      })
    },
    onError(file, fileList) {
      this.fileList.push({
        name: 'hello',
        url: 'https://builtbybuffalo.com/uploads/work/300/1306190728.png'
      })
      this.iconPlusVisible = !this.fileList.length > 0
    },
    onPreview(file) {

    }
  }
}
</script>
<style>
  .avatar-uploader .el-upload {
    border: 1px dashed #d9d9d9;
    border-radius: 6px;
    cursor: pointer;
    position: relative;
    overflow: hidden;
  }
  .avatar-uploader .el-upload:hover {
    border-color: #409EFF;
  }
  .avatar-uploader-icon {
    font-size: 28px;
    color: #8c939d;
    width: 120px;
    height: 120px;
    line-height: 120px;
    text-align: center;
  }
</style>
