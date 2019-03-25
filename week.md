
### Algorithm

LeeCode 链接地址: https://leetcode.com/problems/add-two-numbers/submissions/
``` java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        Integer l1Num = ListNodeToInteger(l1);
        Integer l2Num = ListNodeToInteger(l2);
        Integer result = l1Num + l2Num;
        //System.out.println(result);
        String reverResultStr = new StringBuilder().append(result.intValue()).reverse().toString();
        //System.out.println(reverResultStr);
        return StringToListNode(reverResultStr);
    }

    private String ListNodeToString(ListNode l) {
        StringBuilder numStr = new StringBuilder();
        while (l != null) {
            numStr.append(l.val);
            l = l.next;
        }
        //System.out.println(numStr);
        return numStr.reverse().toString();
    }

    private Integer ListNodeToInteger(ListNode l) {
        return Integer.valueOf(ListNodeToString(l));
    }

    private ListNode StringToListNode(String numStr) {
        int numStart = 48;
        ListNode current = null;
        ListNode head = null;
        int length = numStr.length();
        for (int index=0; index < length; index++) {
            int value = numStr.codePointAt(index) - numStart;
            //System.out.println(value);
            if (current != null) {
                current.next = new ListNode(value);
                current = current.next;
            } else {
                current = new ListNode(value);
                head = current;
            }
        }
        current = null;
        return head;
    }
}
```

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode addTwoNumbers1(ListNode l1, ListNode l2) {
        ListNode tail = new ListNode(0);
        ListNode current = tail;
        while(l1!=null && l2!=null) {
            int ret = l1.val + l2.val;
            current.val = ret%10;
            System.out.println(ret);
            ListNode prev = new ListNode(0);
            prev.next = current;
            prev.val += ret/10;
            current = prev;
            l1 = l1.next;
            l2 = l2.next;
        }
        while (l1!=null) {
            int ret = current.val + l1.val;
            current.val += ret%10;
            ListNode prev = new ListNode(0);
            prev.next = current;
            prev.val = ret/10;
            current = prev;
            l1 = l1.next;
        }
        while (l2!=null) {
            int ret = current.val + l2.val;
            current.val += ret%10;
            ListNode prev = new ListNode(0);
            prev.next = current;
            prev.val = ret/10;
            current = prev;
            l2 = l2.next;
        }
        if (current.val != 1) {
            return current.next;
        } else {
            return current;
        }
    }
}
```

第一种解法直观易理解，第二种解法高效，难理解。

### Review

这周主要看来 OpenFeign 的官方文档和部分代码。具体参考[我的博客](https://blog.csdn.net/wenxueliu/article/details/88730503)


### Tips

第一周推荐一个画图的软件吧，在 Mac 下一直没有找到合适的画图软件，直到遇到
draw.io，好不好，用了就知道了。

### Share

这周在看 DDD 驱动设计。

对 Entity，Value Object，Factory，Repository 有了基本的路径。目前阅读进入 30%。
另外，在领域驱动设计中，最重要的一点架构师和程序员讨论实现细节，让信息在架构师
和程序员之间流动，而不是单向的架构师到程序员流动。这是与之前普遍模型最大的不同之处。
目前，靠回忆能想到这么多。看完之后会整理专门的读书笔记。
