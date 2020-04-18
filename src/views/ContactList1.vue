<template>
  <div class="home">
    <!-- 联系人列表 -->
    <van-contact-list
      :list="list"
      @add="onAdd"
      @edit="onEdit"
    />
    <!-- 联系人编辑 -->
    <van-popup v-model="showEdit" position="bottom">
      <van-contact-edit
        :contact-info="editingContact"
        :is-edit="isEdit"
        @save="onSave"
        @delete="onDelete"
      />
    </van-popup>
  </div>
</template>

<script>
import { ContactList, Toast, ContactEdit, Popup } from 'vant'
export default {
  name: 'contactList',
  components: {
    [ContactList.name]: ContactList,
    [ContactEdit.name]: ContactEdit,
    [Popup.name]: Popup
  },
  data () {
    return {
      list: [],
      instance: null, // axios实例
      showEdit: false, // 编辑弹窗的显隐
      editingContact: {}, // 正在编辑的联系人数据
      isEdit: false // 新建或者编辑
    }
  },
  methods: {
    // 获取联系人列表
    async getList () {
      let res = await this.$Http.getContactList()
      this.list = res.data
    },
    // 添加联系人
    onAdd () {
      this.showEdit = true
      this.isEdit = false
      this.editingContact = {}
    },
    // 编辑联系人
    onEdit (info) {
      this.showEdit = true
      this.isEdit = true
      this.editingContact = info
    },
    // 保存联系人
    async onSave (info) {
      if (this.isEdit) {
        // 编辑保存
        let res = await this.$Http.editContact(info)
        if (res.code === 200) {
          Toast('修改成功')
          this.showEdit = false
          this.getList()
        }
      } else {
        // 新建保存
        // let res = await this.$Http.newContactJson(info)
        // if (res.code === 200) {
        //   Toast('新建成功')
        //   this.showEdit = false
        //   this.getList()
        // }
        let res = await this.$Http.newContactForm(info, true)
        if (res.code === 200) {
          Toast('新建成功')
          this.showEdit = false
          this.getList()
        }
      }
    },
    // 删除联系人
    async onDelete (info) {
      let res = await this.$Http.delContact({
        id: info.id
      })
      if (res.code === 200) {
        Toast('删除成功')
        this.showEdit = false
        this.getList()
      }
    }
  },
  created () {
    this.getList()
  }
}
</script>
