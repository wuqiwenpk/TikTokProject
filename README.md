<div class="modal fade" id="loadingModal" backdrop="static" keyboard="false">
    　　<div style="width: 200px;height:20px; z-index: 2000; position: absolute; text-align: center; left: 50%; top: 50%;margin-left:-100px;margin-top:-10px">
{#    　　　　<div class="progress progress-striped active" style="margin-bottom: 0;">#}
{#    　　　　　　<h5 id="loadText">loading...</h5>#}
{#    　　　　</div>#}
    　　　　<h5 id="loadText" style="color: white">loading...</h5>
    　　</div>
</div>

<script type="text/javascript">
    var loadingTime= 5;//默认遮罩时间
    function showLoading() {
        $('#loadingModal').modal({backdrop: 'static', keyboard: false});
    }
    function hideLoading() {
        $('#loadingModal').modal('hide');
    }
    showLoading()
</script>
