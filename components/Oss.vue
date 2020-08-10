<template>
  <div>
    <el-upload
      ref="aliyunoss"
      :class="optionData.type==='custom'?'custom':''"
      :action="optionData.uploadUrl"
      :headers="optionData.uploadHeader"
      :name="optionData.name"
      :file-list="optionData.fileList"
      :list-type="optionData.listType"
      :multiple="optionData.multiple"
      :limit="optionData.limit"
      :drag="optionData.drag"
      :accept="optionData.accept"
      :auto-upload="optionData.autoUpload"
      :http-request="upload"
      :on-exceed="allowLimit"
      :before-upload="beforeUpload"
      :on-remove="removeFile"
      class="upload-demo"
    >
      <i v-if="optionData.drag" class="el-icon-upload" />
      <div v-if="optionData.drag" class="el-upload__text">将文件拖到此处，或<em>点击上传</em></div>
      <el-button v-if="(optionData.listType==='fileList' || optionData.listType==='picture') && !optionData.drag && optionData.autoUpload" size="small" type="primary" icon="el-icon-plus">点击上传</el-button>
      <i v-else-if="optionData.autoUpload && !optionData.drag" class="el-icon-plus" />
      <el-button v-if="!optionData.autoUpload" slot="trigger" size="small" type="primary">选取文件</el-button>
      <el-button v-if="!optionData.autoUpload" style="margin-left: 10px;" size="small" type="success" @click="submitUpload">上传到服务器</el-button>
      <div slot="tip" class="el-upload__tip">{{ optionData.tip +'  单个文件不超过'+optionData.fileSize+'M' }}</div>
    </el-upload>
  </div>
</template>

<script>
import { mapActions } from 'vuex'
import axios from 'axios'
export default {
  name: 'AliYunOss',

  components: {

  },

  props: {
    option: {
      type: Object,
      default: () => {
        return {
          type: '', // 文件上传样式类型（非el-upload所需）
          fileList: [], // 已上传文件列表  格式 {name:sdf,url:src,fileId:123,uid:1345,status:'success'}
          listType: 'picture-card', // 文件列表展示类型 text/picture/picture-card  启用拖拽上传时 listType为空
          multiple: false, // 允许多选
          limit: 1, // 允许上传数量
          messageErrorNumber: '您已超出最大允许上传数量', // `最多允许上传${this.optionData.limit}个文件，您已超出`, // 文件个数超出
          autoUpload: true, // 是否自动上传
          drag: false, // 是否启用拖拽  启用拖拽后父层调用位置 最小预留高度200px
          accept: 'image/jpg,image/jpeg,image/gif,image/png,image/bmp,', // 文件允许类型格式
          // 图片文件格式: 'image/jpeg,image/gif,image/png,image/bmp,image/tiff,application/x-shockwave-flash,image/svg+xml'
          // 视频文件格式: 'video/mp4,video/x-flv,video/quicktime,video/x-ms-wmv,video/x-ms-asf,video/3gpp,video/avi,video/x-matroska'
          // 音频文件格式: 'audio/mp3,audio/wav,audio/aiff,audio/basic,audio/mpeg,audio/mid,'
          // 安卓安装包: 'application/vnd.android.package-archive'
          // 压缩包格式： 'application/x-zip-compressed,application/x-tar'
          // 文档格式： 'application/pdf,application/msword,application/vnd.openxmlformats-officedocument.wordprocessingml.document,application/vnd.openxmlformats-officedocument.spreadsheetml.sheet,application/vnd.ms-excel'
          fileSize: '5', // 文件大小
          messageErrorFormat: '文件格式不正确，请选择正确格式文件', // 文件格式错误提示
          uploadUrl: '', // 文件上传地址
          name: '', // 上传对应字段名称
          uploadHeader: {}, // 文件上传请求头
          fileCategory: null, // 文件类型【0 :JudgmentDocument 裁判文书,1：AgentWord 代理词，2：OtherCaseFile 案件其他材料,3：Avatar 头像,4：LawyerLicence 律师执业证,】
          tip: '只能上传jpg/png/bmp/gif文件',
          messageSuccess: '文件上传成功'
        }
      }
    }
  },
  data() {
    return {
      // 上传控件参数
      optionData: {
        type: '', // 文件上传样式类型（非el-upload所需）
        fileList: [], // 已上传文件列表  格式 {name:sdf,url:src}
        listType: 'picture-card', // 文件列表展示类型 text/picture/picture-card  启用拖拽上传时 listType为空
        multiple: false, // 允许多选
        limit: 1, // 允许上传数量
        messageErrorNumber: '您已超出最大允许上传数量', // `最多允许上传${this.optionData.limit}个文件，您已超出`, // 文件个数超出
        autoUpload: true, // 是否自动上传
        drag: false, // 是否启用拖拽  启用拖拽后父层调用位置 最小预留高度200px
        accept: 'image/jpg,image/jpeg,image/gif,image/png,image/bmp,', // 文件允许类型格式
        // 图片文件格式: 'image/jpeg,image/gif,image/png,image/bmp,image/tiff,application/x-shockwave-flash,image/svg+xml'
        // 视频文件格式: 'video/mp4,video/x-flv,video/quicktime,video/x-ms-wmv,video/x-ms-asf,video/3gpp,video/avi,video/x-matroska'
        // 音频文件格式: 'audio/mp3,audio/wav,audio/aiff,audio/basic,audio/mpeg,audio/mid,'
        // 安卓安装包: 'application/vnd.android.package-archive'
        // 压缩包格式： 'application/x-zip-compressed,application/x-tar'
        // 文档格式： 'application/pdf,application/msword,application/vnd.openxmlformats-officedocument.wordprocessingml.document,application/vnd.openxmlformats-officedocument.spreadsheetml.sheet,application/vnd.ms-excel'
        fileSize: '5', // 文件大小
        messageErrorFormat: '文件格式不正确，请选择正确格式文件', // 文件格式错误提示
        uploadUrl: '', // 文件上传地址
        name: '', // 上传对应字段名称
        uploadHeader: {}, // 文件上传请求头
        fileCategory: null, // 文件类型【0 :JudgmentDocument 裁判文书,1：AgentWord 代理词，2：OtherCaseFile 案件其他材料,3：Avatar 头像,4：LawyerLicence 律师执业证,】
        tip: '只能上传jpg/png文件',
        messageSuccess: '文件上传成功'
      }
    }
  },

  watch: {
    option: {
      immediate: true,
      deep: true,
      handler(val) {
        for (const item in val) {
          this.optionData[item] = val[item]
        }
      }
    }
  },

  mounted() {
  },

  methods: {
    ...mapActions('file', ['OssSignature']),
    // 自定义上传文件获取签名
    upload(file) {
      const fileData = { FileName: file.file.name, fileCategory: this.optionData.fileCategory }
      this.OssSignature(fileData).then(res => {
        this.uploadFile(file, res)
      })
    },
    // 开始文件上传
    uploadFile(file, header) {
      // 将签名成功后数据组合成为formData格式
      const data = new FormData()
      for (const item in header) {
        data.append(item, header[item])
      }
      // 将文件数据添加至 formData 格式数据中
      data.append('File', file.file)

      // axios 请求 config
      const config = {
        headers: {
          contentType: 'multipart/form-data' // 发送请求内容数据类型
        },
        // 进度条
        onUploadProgress: progressEvent => {
          var complete = (progressEvent.loaded / progressEvent.total * 100 | 0) // + '%'
          file.onProgress({ percent: complete }) // 手动调用文件上传进度条
        }
      }
      // 发送 上传文件请求
      axios.post(header.host, data, config).then(res => {
        res.data.isSucceed ? this.uploadSuccess(res, file) : this.$notify.error(`提示：${res.data.message}`)
      })
    },

    // 最大文件数验证
    allowLimit(files) {
      if (files.length >= this.optionData.limit) {
        this.$notify.error('最多允许上传' + this.optionData.limit + '个文件!')
      }
    },

    // 上传之前文件格式
    beforeUpload(file) {
      const maxSize = this.optionData.fileSize * 1024 * 1024
      const inSize = maxSize > file.size
      const isType = this.optionData.accept !== '' & file.type !== '' ? this.optionData.accept.split(',').indexOf(file.type) >= 0 : file.type !== ''
      isType ? inSize ? '' : this.$notify.error('提示：上传文件大小超出最大允许限制') : this.$notify.error(`提示：${this.optionData.messageErrorFormat}`)
      return isType && inSize
    },
    // 文件上传成功
    uploadSuccess(response, file, filelist) {
      this.$notify.success(`提示：${this.optionData.messageSuccess}`)
      this.optionData.fileList.push({ name: file.file.name, url: response.data.data.path, fileId: response.data.data.fileId })
      this.$emit('change', this.optionData.fileList)
    },
    // 文件上传失败
    uploadError(err, file, fileList) {
      const error = JSON.parse(err.message)
      if (error.error) {
        this.$notify.error(error.error.message)
      } else {
        this.$notify.error(error.result.message)
      }
    },
    // 移除已上传文件
    removeFile(file) {
      this.optionData.fileList.forEach((item, index) => {
        item.fileId === file.fileId ? this.optionData.fileList.splice(index, 1) : ''
      })
      this.$emit('change', this.optionData.fileList)
    },
    // 非自动上传提交方法
    submitUpload() {
      this.$refs.aliyunoss.submit()
    }
  }
}
</script>

<style lang='scss'>
.el-upload__tip{
  line-height: normal;
}
.custom{
  .el-upload-list{
    display: none
  }

}
</style>
