```php

//==============================001题==============================
/* 给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的 两个 整数。
 * 你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。
 * 给定 nums = [2, 7, 11, 15], target = 9
 * 因为 nums[0] + nums[1] = 2 + 7 = 9
 * 所以返回 [0, 1]
 */
function twoSum($arr, $target = 0)
{
    //判断数组的可靠性
    if (!is_array($arr) || empty($arr)) {
        return [];
    }

    //记录两个key
    $hashList = [];

    //循环数据得到数据
    foreach ($arr as $key => $val) {
        $tmp = $target - $val;
        if (isset($hashList[$tmp])) {
            return [$hashList[$tmp], $key];
        }
        $hashList[$val] = $key;
    }
}

$arr = [2, 7, 8, 9];
print_r(twoSum($arr, 11));

//==============================002题==============================
/* 在一个二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。
 * 请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数
 */
function existTwoDimensional($arr = [], $number = 0)
{
    if (empty($arr) || !is_array($arr)) {
        return false;
    }

    $rows = count($arr);//共rows行
    $cols = count($arr[0]);//共cols列
    if ($rows > 0 && $cols > 0) {
        $row = 0;
        $col = $cols - 1;
        while ($row < $rows && $col >= 0) {
            if ($number == $arr[$row][$col]) {
                return true;
            } elseif ($number < $arr[$row][$col]) {
                $col -= 1;
            } else {
                $row += 1;
            }
        }

        return false;
    }

    return false;
}

$arr = [
    [1, 2, 3, 4, 5],
    [2, 3, 4, 5, 6],
    [3, 4, 5, 6, 7],
    [9, 10, 11, 12, 13]
];

print_r(existTwoDimensional($arr, 11));

//==============================003题==============================
/* 给出两个 非空 的链表用来表示两个非负的整数。其中，它们各自的位数是按照 逆序 的方式存储的，
 * 并且它们的每个节点只能存储 一位 数字。如果，我们将这两个数相加起来，
 * 则会返回一个新的链表来表示它们的和。您可以假设除了数字 0 之外，这两个数都不会以 0 开头。
 * 输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
 * 输出：7 -> 0 -> 8
 * 原因：342 + 465 = 807
 */
function addTwoNumbers($arr1 = [], $arr2 = [])
{
    if (empty($arr1) || empty($arr2)) {
        return [];
    }

    //新的链表
    $newArr = [];

    //计算那个链表最长
    $longest = count($arr1) > count($arr2) ? count($arr1) : count($arr2);

    //计算是否有进位 0没有进位 1有进位
    $flag = 0;
    for ($i = 0; $i < $longest; $i++) {
        $tmp1 = $arr1[$i] ?? 0;
        $tmp2 = $arr2[$i] ?? 0;
        //计算总和
        $sum = $tmp1 + $tmp2 + $flag;
        //计算出余数
        $newArr[$i] = $sum % 10;
        //计算出是否需要进位
        $flag = $sum / 10;
    }

    if ($flag > 0) {
        $newArr[] = 1;
    }

    return $newArr;
}

$arr1 = [1, 2, 3];
$arr2 = [9, 9, 9];
print_r(addTwoNumbers($arr1, $arr2));

//==============================004题==============================
/* 给定一个字符串，请你找出其中不含有重复字符的 最长子串 的长度。
 * 输入: "abcabcbb"
 * 输出: 3
 * 解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
 * 输入: "bbbbb"
 * 输出: 1
 * 解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
 */
function lengthOfLongestSubstring($str = '')
{
    if (empty($str)) {
        return 0;
    }

    $arr = [];//存在的字符串
    $maxl = $left = 0;
    $length = strlen($str);
    for ($i = 0; $i < $length; $i++) {
        if (isset($arr[$str[$i]]) && $left <= $arr[$str[$i]]) {
            $left = $arr[$str[$i]] + 1;
        } else {
            $maxl = max($maxl, $i - $left + 1);
        }

        echo $maxl . '----' . $left . "<br>";
        $arr[$str[$i]] = $i;
    }

    return $maxl;
}

$str = 'abcedddedd';
echo lengthOfLongestSubstring($str);

```
