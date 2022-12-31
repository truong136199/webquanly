<template>
  <div>
    <div v-show="isThongBaoThemThanhCong" class="alert alert-success">
    <strong>Thành công!</strong> Thêm thành công.
    </div>
    <div v-show="isThongBaoThemBiTrung" class="alert alert-warning">
    <strong>Warning!</strong> ID bị trùng .
  </div>
   <div style="margin-top: 40px; text-align: left">
     <input type="text" placeholder="Mã Sản Phẩm" v-model="khoa.maSanPham" @keyup.enter="search" style="width: 170px">
     <input type="text" placeholder="Tên Sản Phẩm " v-model="khoa.tenSanPham" @keyup.enter="search" style="width: 170px">
     <input type="text" placeholder="Thông Tin Sản Phẩm " v-model="khoa.thongTinSanPham" @keyup.enter="search" style="width: 170px">
     <button class="btn btn-info" @click="search" style="margin-left: 50px; width: 100px">Tìm kiếm</button>
     <button class="btn btn-info" @click="resetSearch" style="margin-left: 10px; width: 100px">Xoá</button>
   </div>
   <div>
     <button type="button" class="btn btn-primary" style="float: right"
     data-bs-toggle="modal" data-bs-target="#doiTuong0">Thêm mới</button>
   </div>
   <div class="btn-group">
  <button type="button" class="btn btn-primary dropdown-toggle" style="float: right" data-bs-toggle="dropdown" aria-expanded="false">
    Xếp Hạng Sản Phẩm
  </button>
  <ul class="dropdown-menu dropdown-menu-dark">
    <li><a class="dropdown-item" >
      <span @click="sanPhamDuoi10Trieu">
        Sản Phẩm Dưới 10 Triệu
    </span></a></li>
    <li><a class="dropdown-item">
      <span @click="sanPhamTu10Den15">
      Giá Từ 10 --> 15 Triệu</span></a></li>
    <li><a class="dropdown-item" >
      <span @click="sanPhamTu15Den20">
      Giá Từ 15 --> 20 Triệu</span></a></li>
    <li><a class="dropdown-item" >
      <span @click="sanPhamTu20Den25">
      Giá Từ 20 --> 25 Triệu</span></a></li>
    <li><a class="dropdown-item" >
      <span @click="sanPhamTu25Den30">
      Giá Từ 25 --> 30 Triệu</span></a></li>
    <li><a class="dropdown-item" >
      <span @click="sanPhamTren30">
      Sản Phẩm Trên 30 Triệu</span></a></li>
  </ul>
</div>
<div class="btn-group">
  <button type="button" class="btn btn-primary dropdown-toggle" style="float: right" data-bs-toggle="dropdown" aria-expanded="false">
    Phân Loại Sản Phẩm
  </button>
  <ul class="dropdown-menu dropdown-menu-dark">
    <li><a class="dropdown-item" >
      <span @click="timKiemDienThoai">
      Sản Phẩm Điện Thoại</span></a></li>
    <li><a class="dropdown-item" >
      <span @click="timKiemMayTinh">
      Sản Phẩm Máy Tính</span></a></li>
    <li><a class="dropdown-item" >
      <span @click="timKiemIpad">
      Sản Phẩm Ipad</span></a></li>
  </ul>
</div>
<div class="btn-group">
  <button type="button" class="btn btn-primary dropdown-toggle" style="float: right" data-bs-toggle="dropdown" aria-expanded="false">
    Số Lượng Sản Phẩm
  </button>
  <ul class="dropdown-menu dropdown-menu-dark">
    <li><a class="dropdown-item" >
      <span @click="top5SPItNhat">
      5 SP có số lượng ít nhất</span></a></li>
    <li><a class="dropdown-item" >
      <span @click="top10SPItNhat">
      10 SP có số lượng ít nhất</span></a></li>
    <li><a class="dropdown-item" >
      <span @click="top5SPNhieuNhat">
      5 SP có số lượng nhiều nhất</span></a></li>
    <li><a class="dropdown-item" >
      <span @click="top10SPNhieuNhat">
      10 SP có số lượng nhiều nhất</span></a></li>
  </ul>
</div>
   <div>
    <table class="table">
  <thead class="thead-dark">
    <tr>
      <th scope="col">STT</th>
      <th scope="col">Mã Sản Phẩm</th>
      <th scope="col">Tên Sản Phẩm</th>
      <th scope="col">Giá Sản Phẩm</th>
      <th scope="col">Số Lượng</th>
      <th scope="col">Thời Gian Tạo</th>
      <th scope="col">Thời Gian Cập Nhập</th>
      <th scope="col">Thao Tác</th>
    </tr>
  </thead>
   <tbody>
     <tr v-for="(data, index) in thongTinCuaSanPhamg" :key="index" >
      <td>{{index + 1}}</td>
        <td>{{data.maSanPham}}</td>
        <td>{{data.tenSanPham}}</td>
        <td>{{data.giaSanPham}}</td>
        <td>{{data.soLuong}}</td>
        <td>{{data.thoiGianTao}}</td>
        <td>{{data.thoiGianCapNhap}}</td>
         <td>
           <div>
             <button @click="timTheoId(data.idTuTang)"
             data-bs-toggle="modal" data-bs-target="#doiTuong3"
             type="button" class="btn btn-primary"
 
                     style="background-color: ; margin-right: 5px">Xem
             </button>
             <button @click="timTheoId(data.idTuTang)"
             type="button" class="btn btn-primary"
             data-bs-toggle="modal" data-bs-target="#doiTuong1"
                     style="background-color: ; margin-right: 5px">Sửa
             </button>
             <button @click="timTheoId(data.idTuTang)"
             style="background-color: " type="button"  class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#doiTuong2"
                      >Xóa
             </button>
           </div>
         </td>
       </tr>
   </tbody>
</table>  
<div>
  <ul class="pagination" style="display: flex">
        <li class="page-item ">
          <a class="page-link" href="#" tabindex="-1" @click="setPage(currentPage)">Previous</a>
        </li>
        <li v-for="page in totalPages" :class="{'page-item': true, 'active': currentPage + 1 === page}" ><a class="page-link" @click="setPage(page)">{{page}}</a></li>       
        <li class="page-item">
          <a class="page-link" href="#" @click="setPage(currentPage + 2)">Next</a>
        </li>
      </ul>
</div>
   <!-- Modal add-->
   <div class="modal fade" id="doiTuong0" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
       <div class="modal-dialog">
         <div class="modal-content">
           <div class="modal-header">
             <h5 class="modal-title" id="exampleModalLabel">Thêm Sản Phẩm Mới</h5>
             <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
           </div>
           <div class="modal-body">
             <div>
               <h6 style="color: green">Mã Sản Phẩm</h6>
               <input type="text" placeholder="Nhập Mã Sản Phẩm: " class="form-control" v-model="sanPham.maSanPham" @blur="validate_maSanPham()" v-bind:class="{'is-invalid': errors.maSanPham}">
               <div class="invalid-feedback" v-if="errors.maSanPham">{{ errors.maSanPham }}</div>
             </div>
             <div>
               <h6 style="color: green">Tên Sản Phẩm</h6>
               <input type="text" placeholder="Nhập Tên Sản Phẩm: " class="form-control" v-model="sanPham.tenSanPham" @blur="validate_tenSanPham()" v-bind:class="{'is-invalid': errors.tenSanPham}">
               <div class="invalid-feedback" v-if="errors.tenSanPham">{{ errors.tenSanPham }}</div>
             </div>
             <div>
               <h6 style="color: green">Thông Tin Sản Phẩm</h6>
               <input type="text" placeholder="Nhập Thông Tin Sản Phẩm: " class="form-control" v-model="sanPham.thongTinSanPham" @blur="validate_thongTinSanPham()" v-bind:class="{'is-invalid': errors.thongTinSanPham}" >
                      <div class="invalid-feedback" v-if="errors.thongTinSanPham">{{ errors.thongTinSanPham }}</div>
             </div>
             <div>
               <h6 style="color: green">Giá Sản Phẩm</h6>
               <input type="text" placeholder="Nhập Giá Sản Phẩm: " class="form-control" v-model="sanPham.giaSanPham" @blur="validate_giaSanPham()" v-bind:class="{'is-invalid': errors.giaSanPham}">
                      <div class="invalid-feedback" v-if="errors.giaSanPham">{{ errors.giaSanPham }}</div>
             </div>
             <div>
               <h6 style="color: green">Số Lượng</h6>
               <input type="text" placeholder="Nhập Số Lượng: " class="form-control" v-model="sanPham.soLuong" @blur="validate_soLuong()" v-bind:class="{'is-invalid': errors.soLuong}">
               <div class="invalid-feedback" v-if="errors.soLuong">{{ errors.soLuong }}</div>
             </div>
             <div>
               <h6 style="color: green">Thời Gian Tạo</h6>
               <input type="text" placeholder="Nhập Thời Gian Tạo: " class="form-control" v-model="sanPham.thoiGianTao" @blur="validate_thoiGianTao()" v-bind:class="{'is-invalid': errors.thoiGianTao}">
                      <div class="invalid-feedback" v-if="errors.thoiGianTao">{{ errors.thoiGianTao }}</div>
             </div>
           
             <div>
               <h6 style="color: green">Thời Gian Cập Nhập</h6>
               <input type="text" placeholder="Nhập Thời Gian Cập Nhập: " class="form-control" v-model="sanPham.thoiGianCapNhap" @blur="validate_thoiGianCapNhap()" v-bind:class="{'is-invalid': errors.thoiGianCapNhap}">
                      <div class="invalid-feedback" v-if="errors.thoiGianCapNhap">{{ errors.thoiGianCapNhap }}</div>
             </div>
           </div>
           <div class="modal-footer">
             <button type="button" class="btn btn-secondary" data-bs-dismiss="modal" @click="resetForm">Đóng</button>
             <button @click="themSanPham"  type="button" class="btn btn-primary" data-bs-dismiss="modal">Thêm Sản Phẩm
             </button>
           </div>
         </div>
       </div>
     </div>
     <!--Modal sua-->
     <div class="modal fade" id="doiTuong1" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
       <div class="modal-dialog">
         <div class="modal-content">
           <div class="modal-header">
             <h5 class="modal-title" id="exampleModalLabel">Sửa Sản Phẩm</h5>
             <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
           </div>
           <div class="modal-body">
             <div>
               <h6 style="color: green">Mã Sản Phẩm</h6>
               <input type="text" placeholder="Nhập Mã Sản Phẩm: " class="form-control" v-model="sanPham.maSanPham">
             </div>
             <div>
               <h6 style="color: green">Tên Sản Phẩm</h6>
               <input type="text" placeholder="Nhập Tên Sản Phẩm: " class="form-control"
                      v-model="sanPham.tenSanPham">
             </div>
             <div>
               <h6 style="color: green">Thông Tin Sản Phẩm</h6>
               <input type="text" placeholder="Nhập Thông Tin Sản Phẩm: " class="form-control"
                      v-model="sanPham.thongTinSanPham">
             </div>
             <div>
               <h6 style="color: green">Giá Sản Phẩm</h6>
               <input type="text" placeholder="Nhập Giá Sản Phẩm: " class="form-control"
                      v-model="sanPham.giaSanPham">
             </div>
             <div>
               <h6 style="color: green">Số Lượng</h6>
               <input type="text" placeholder="Nhập Số Lượng: " class="form-control" v-model="sanPham.soLuong">
             </div>
             <div>
               <h6 style="color: green">Thời Gian Tạo</h6>
               <input type="text" placeholder="Nhập Thời Gian Tạo : " class="form-control"
                      v-model="sanPham.thoiGianTao">
             </div>
           
             <div>
               <h6 style="color: green">Thời Gian Cập Nhập</h6>
               <input type="text" placeholder="Nhập Thời Gian Cập Nhập : " class="form-control"
                      v-model="sanPham.thoiGianCapNhap">
             </div>
           </div>
           <div class="modal-footer">
             <button type="button" class="btn btn-secondary" data-bs-dismiss="modal" @click="resetForm">Đóng</button>
             <button type="button" class="btn btn-primary" data-bs-dismiss="modal" @click="suaSanPham" >Chỉnh Sửa
             </button>
           </div>
         </div>
       </div>
     </div>
     <!--Modal xoa-->
     <div class="modal fade" id="doiTuong2" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
       <div class="modal-dialog">
         <div class="modal-content">
           <div class="modal-header">
             <h5 class="modal-title" id="exampleModalLabel">Thông báo</h5>
             <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
           </div>
           <div class="modal-body">
             <h3>Bạn Có Muốn Xoá Sản Phẩm Này Không ?</h3>
           </div>
           <div class="modal-footer">
             <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Đóng</button>
             <button type="button" class="btn btn-primary" data-bs-dismiss="modal" @click="xoasanPham">Xoá Sản Phẩm
             </button>
           </div>
         </div>
       </div>
     </div>
      <!--Modal xem-->
      <div class="modal fade" id="doiTuong3" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
       <div class="modal-dialog">
         <div class="modal-content">
           <div class="modal-header">
             <h5 class="modal-title" id="exampleModalLabel">Xem chi tiết người dùng</h5>
             <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
           </div>
           <div class="modal-body">
             <div>
               <h6 style="color: green">Mã Sản Phẩm</h6>
               <input type="text" placeholder="Nhập Mã Sản Phẩm: " class="form-control" v-model="sanPham.maSanPham">
             </div>
             <div>
               <h6 style="color: green">Tên Sản Phẩm</h6>
               <input type="text" placeholder="Nhập Tên Sản Phẩm: " class="form-control"
                      v-model="sanPham.tenSanPham">
             </div>
             <div>
               <h6 style="color: green">Thông Tin Sản Phẩm</h6>
               <input type="text" placeholder="Nhập Thông Tin Sản Phẩm: " class="form-control"
                      v-model="sanPham.thongTinSanPham">
             </div>
             <div>
               <h6 style="color: green">Giá Sản Phẩm</h6>
               <input type="text" placeholder="Nhập Giá Sản Phẩm: " class="form-control"
                      v-model="sanPham.giaSanPham">
             </div>
             <div>
               <h6 style="color: green">Số Lượng</h6>
               <input type="text" placeholder="Nhập Số Lượng: " class="form-control" v-model="sanPham.soLuong">
             </div>
             <div>
               <h6 style="color: green">Thời Gian Tạo</h6>
               <input type="text" placeholder="Nhập Thời Gian Tạo : " class="form-control"
                      v-model="sanPham.thoiGianTao">
             </div>
           
             <div>
               <h6 style="color: green">Thời Gian Cập Nhập</h6>
               <input type="text" placeholder="Nhập Thời Gian Cập Nhập : " class="form-control"
                      v-model="sanPham.thoiGianCapNhap">
             </div>
           </div>
           <div class="modal-footer">
             <button type="button" class="btn btn-secondary" data-bs-dismiss="modal" @click="resetForm">Đóng</button>
           </div>
         </div>
       </div>
     </div>
  </div>
  </div>
  
 </template>
 <script>
 import axios from 'axios';
 export default {
   data() {
     return {
       thongTinCuaSanPhamg: [],
       isThongBaoThemThanhCong: false,
       isThongBaoThemBiTrung: false,
       currentPage: 0,
       totalPages: [],
       sanPham: {
        idTuTang : '',
         maSanPham : '',
         tenSanPham : '',
         thongTinSanPham : '',
         giaSanPham : '',
         soLuong : '',
         thoiGianTao : '',
         thoiGianCapNhap : ''
       },
       errors: {
         maSanPham : '',
         tenSanPham : '',
         thongTinSanPham : '',
         giaSanPham : '',
         soLuong : '',
         thoiGianTao : '',
         thoiGianCapNhap : ''
       },
       idSanPham : '',
       khoa:{
         maSanPham: '',
         tenSanPham:'',
         thongTinSanPham:'',
         soLuong:'',
         thoiGianCapNhap:''
       },
       }
   },
   methods: {
    sanPhamDuoi10Trieu() {
      axios.get(`http://localhost:8080/api/v1/quanlybanhang/duoi10`)
                .then(res=> {
                  this.thongTinCuaSanPhamg = res.data
                })
        },
    sanPhamTu10Den15() {
      axios.get(`http://localhost:8080/api/v1/quanlybanhang/tu10den15`)
                .then(res=> {
                  this.thongTinCuaSanPhamg = res.data
                })
        },
    sanPhamTu15Den20() {
      axios.get(`http://localhost:8080/api/v1/quanlybanhang/tu15den20`)
                .then(res=> {
                  this.thongTinCuaSanPhamg = res.data
                })
        },
    sanPhamTu20Den25() {
      axios.get(`http://localhost:8080/api/v1/quanlybanhang/tu20den25`)
                .then(res=> {
                  this.thongTinCuaSanPhamg = res.data
                })
        },
    sanPhamTu25Den30() {
      axios.get(`http://localhost:8080/api/v1/quanlybanhang/tu25den30`)
                .then(res=> {
                  this.thongTinCuaSanPhamg = res.data
                })
        },
    sanPhamTren30() {
      axios.get(`http://localhost:8080/api/v1/quanlybanhang/tren30`)
                .then(res=> {
                  this.thongTinCuaSanPhamg = res.data
                })
        },
    timKiemDienThoai() {
      axios.get(`http://localhost:8080/api/v1/quanlybanhang/dienthoai`)
                .then(res=> {
                  this.thongTinCuaSanPhamg = res.data
                })
        },                    
    timKiemMayTinh() {
      axios.get(`http://localhost:8080/api/v1/quanlybanhang/maytinh`)
                .then(res=> {
                  this.thongTinCuaSanPhamg = res.data
                })
        }, 
    timKiemIpad() {
      axios.get(`http://localhost:8080/api/v1/quanlybanhang/ipad`)
                .then(res=> {
                  this.thongTinCuaSanPhamg = res.data
                })
        },
    top5SPItNhat() {
      axios.get(`http://localhost:8080/api/v1/quanlybanhang/5spitnhat`)
                .then(res=> {
                  this.thongTinCuaSanPhamg = res.data
                })
        },
    top10SPItNhat() {
      axios.get(`http://localhost:8080/api/v1/quanlybanhang/10spitnhat`)
                .then(res=> {
                  this.thongTinCuaSanPhamg = res.data
                })
        },
    top5SPNhieuNhat() {
      axios.get(`http://localhost:8080/api/v1/quanlybanhang/5spnhieunhat`)
                .then(res=> {
                  this.thongTinCuaSanPhamg = res.data
                })
        },
    top10SPNhieuNhat() {
      axios.get(`http://localhost:8080/api/v1/quanlybanhang/10spnhieunhat`)
                .then(res=> {
                  this.thongTinCuaSanPhamg = res.data
                })
        },
    setPage(page) {
            if(page >= 0){
                this.currentPage = page - 1;
                this.findAll()
            }
        },
        findAll() {
            axios.get(`http://localhost:8080/api/v1/quanlybanhang?page=${this.currentPage}`)
                .then(res=> {
                  this.thongTinCuaSanPhamg = res.data.content
                })
        },
     resetForm() {
     this.sanPham = {
         maSanPham : '',
         tenSanPham : '',
         thongTinSanPham : '',
         giaSanPham : '',
         soLuong : '',
         thoiGianTao : '',
         thoiGianCapNhap : ''
       }
     },
     themSanPham() {
       if (this.validate()){
       axios.post("http://localhost:8080/api/v1/quanlybanhang",this.sanPham).then(res => {
         this.resetForm()
         this.findAll()
         this.sanPham = {}
         if(res.data.thongBao === 'them thanh cong') {
          this.isThongBaoThemThanhCong = true
          setTimeout(() => {
            this.isThongBaoThemThanhCong = false
          }, 4000);
         }
         else {
          this.isThongBaoThemBiTrung = true
          setTimeout(() => {
            this.isThongBaoThemBiTrung = false
          }, 4000);
         }
       })
     }
     },
     timTheoId(idTuTang){
       axios.get("http://localhost:8080/api/v1/quanlybanhang/" + idTuTang).then((res) => {
         this.idSanPham = idTuTang
         this.sanPham = {
         maSanPham : res.data.maSanPham,
         tenSanPham : res.data.tenSanPham,
         thongTinSanPham : res.data.thongTinSanPham,
         giaSanPham : res.data.giaSanPham,
         soLuong : res.data.soLuong,
         thoiGianTao : res.data.thoiGianTao,
         thoiGianCapNhap : res.data.thoiGianCapNhap
       }
       })
     },
     suaSanPham(){
       axios.put("http://localhost:8080/api/v1/quanlybanhang/" + this.idSanPham, this.sanPham).then((res) => {
       // this.showMessage('succes','Edit!','Sửa thành công')
       this.resetForm()
       this.findAll()
     })
     },
     xoasanPham(){
       axios.delete("http://localhost:8080/api/v1/quanlybanhang/" + this.idSanPham).then((res) => {
        this.findAll()
       })
     },
     search(){
      axios.get(`http://localhost:8080/api/v1/quanlybanhang/search?page=${this.currentPage}`,{
        params: {
          maSanPham: this.khoa.maSanPham,
          tenSanPham: this.khoa.tenSanPham,
          thongTinSanPham: this.khoa.thongTinSanPham,
        }
       }).then(res => {
         this.thongTinCuaSanPhamg = res.data
       })
     },
     resetSearch(){
       this.khoa = {
         maSanPham:'',
         tenSanPham:'',
         thongTinSanPham:'',
         soLuong:'',
         thoiGianCapNhap:'',
       }
       this.search()
     },
     validate_maSanPham(){
       this.errors.maSanPham = ''
       if(!this.sanPham.maSanPham){
         this.errors.maSanPham = 'Mã Sản Phẩm không được để trống'
         return false
       }
       return true
     },
     validate_tenSanPham(){
       this.errors.tenSanPham = ''
       if(!this.sanPham.tenSanPham){
         this.errors.tenSanPham = 'Tên sản phẩm không được để trống'
         return false
       }
       return true
     },
     validate_thongTinSanPham(){
       this.errors.thongTinSanPham = ''
       if(!this.sanPham.thongTinSanPham){
         this.errors.thongTinSanPham = 'Thông Tin Sản Phẩm không được để trống'
         return false
       }
       return true
     },
     validate_giaSanPham(){
       this.errors.giaSanPham = ''
       if(!this.sanPham.giaSanPham){
         this.errors.giaSanPham = 'Giá Sản Phẩm không được để trống'
         return false
       }
       if (this.sanPham.giaSanPham < 0) {
         this.errors.giaSanPham = 'Giá sản phẩm không được âm'
         return false
       }
       return true
     },
     validate_soLuong(){
       this.errors.soLuong = ''
       if(!this.sanPham.soLuong){
         this.errors.soLuong = 'Số Lượng không được để trống'
         return false
        }
       if (this.sanPham.soLuong < 0) {
         this.errors.soLuong = 'Số lượng không được âm'
         return false
       }
       return true
       
      },
     validate_thoiGianTao(){
       this.errors.thoiGianTao = ''
       if(!this.sanPham.thoiGianTao){
         this.errors.thoiGianTao = 'thời gian tạo không được để trống'
         return false
       }
       
       return true
     },
     validate_thoiGianCapNhap(){
       this.errors.thoiGianCapNhap = ''
       if(!this.sanPham.thoiGianCapNhap){
         this.errors.thoiGianCapNhap = 'Thời gian cập nhập không được để trống'
         return false
       }
       return true
     },
     validate(){
       if(!this.validate_maSanPham() ||
          !this.validate_tenSanPham() ||
          !this.validate_thongTinSanPham() ||
          !this.validate_giaSanPham() ||
          !this.validate_soLuong() ||
          !this.validate_thoiGianTao() ||
          !this.validate_thoiGianCapNhap())
           return false
         return true
     }
     //   showMessage(icon, title, text) {
     //   this.$swal.fire({
     //     showConfirmButton: false,
     //     timer: 2000,
     //     icon: icon,
     //     title: title,
     //     text: text
     //   });
     // },
 
   },
   created(){
     axios.get('http://localhost:8080/api/v1/quanlybanhang').then((res) => {
       for(let i = 0; i < res.data.totalPages; i++) {
         this.totalPages.push(i+1)
       }
       this.thongTinCuaSanPhamg = res.data.content
     })
   },
  
 
 }
 </script>
 
 <style scoped>
 
 </style>