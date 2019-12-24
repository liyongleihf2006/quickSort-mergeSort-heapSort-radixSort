# quickSort-mergeSort-heapSort-radixSort

*非递归 快速排序 归并排序 堆排序 基数排序 的实现*

```js
//快速排序
function quickSort(arr){
    var parts  = [[0,arr.length-1]];
    while(parts .length){
        var part = parts .shift();
        var l = part[0];
        var r = part[1];
        if(l>=r){
            continue;
        }
        var midx = l;
        var mid = arr[midx];
        for(var i = l+1;i<=r;i++){
            if(arr[i]<mid){
                var temp = arr.splice(i,1);
                arr.splice(l,0,...temp);
                midx = i;
            }
        }
        parts .push([l,midx-1],[midx+1,r]);
    }
}
//归并排序
function mergeSort(arr) {
    var temp = [];
    for (var length = 2; length / 2 <= arr.length; length *= 2) {
        for (var start = 0; start < arr.length; start += length) {
            wrap(start, start + length - 1, temp);
        }
    }
    function wrap(begin, end, temp) {
        var mid = Math.floor((begin + end) / 2);
        var i = begin;
        var a = mid;
        var j = mid + 1;
        var b = end;
        var k = 0;
        while (i <= a && i <= arr.length - 1 && j <= b && j <= arr.length - 1) {
            arr[i] > arr[j] ? temp[k++] = arr[i++] : temp[k++] = arr[j++];
        };
        while (i <= a && i <= arr.length - 1) {
            temp[k++] = arr[i++];
        };
        while (j <= b && j <= arr.length - 1) {
            temp[k++] = arr[j++];
        };
        for (var kk = 0; kk < k; kk++) {
            arr[begin + kk] = temp[kk];
        }
    }
}
//堆排序
function heapSort(arr) {
    for (var i = arr.length - 1; i > 0; i--) {
        sort(i);
        adjust(i);
    }
    function sort(i) {
        var p = Math.floor((i - 1) / 2);
        while (p >= 0) {
            var l = 2 * p + 1;
            var r = l + 1;
            var max = l;
            var temp;
            if (r <= i && arr[r] > arr[l]) {
                max = r;
            }
            temp = arr[max];
            if (temp > arr[p]) {
                arr[max] = arr[p];
                arr[p] = temp;
            }
            p--;
        }
    }
    function adjust(i) {
        var temp = arr[i];
        arr[i] = arr[0];
        arr[0] = temp;
    }
}
//基数排序
function radixSort(arr,d){
    var radixArray=[[],[],[],[],[],[],[],[],[],[]];
    var bit = -1;
    while(bit++<=d){
        arr.forEach(function(item){
            var idx = Math.floor(item/Math.pow(10,bit))%10;
            radixArray[idx].push(item);
        });
        arr.length=0;
        radixArray.forEach(function(a){
            a.forEach(function(item){
               arr.push(item); 
            });
            a.length=0;
        });
    }
}
```


