- since all lists are sorted, each head node from each list is the smallest of each list, and by keeping them in a min heap, the smallest of all smallests will be the global smallest. 
- using a special data structure to track each globally smallest number 

```cpp
struct comp{
        bool operator()(ListNode *a, ListNode *b){ //this will result a min heap since bigger nums are more prioritized
            return a->val > b->val;
        }
    };
    
ListNode* mergeKLists(vector<ListNode*>& lists) {
    if (lists.empty()) return NULL;

    priority_queue<ListNode*, vector<ListNode*>, comp>pq; 
    ListNode *dummy = new ListNode(0), *head = dummy;

    //because there is no such thing as all columns are sorted 
    for (auto node:lists){
        if (node)
            pq.push(node);
    }
    while(!pq.empty()){
        ListNode *curr = pq.top();
        pq.pop();
        head->next = curr;
        head = head->next;
        if (curr->next)
            pq.push(curr->next);
    }

    head = dummy->next;
    delete dummy;
    return head;
}
  ```

