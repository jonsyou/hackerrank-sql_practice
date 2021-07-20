> Practice > SQL > Advanced Select > Binary Tree Nodes
# Binary Tree Nodes [link](https://www.hackerrank.com/challenges/binary-search-tree-1/problem)

You are given a table, BST, containing two columns: N and P, where N represents the value of a node in Binary Tree, and P is the parent of N.

![image](https://user-images.githubusercontent.com/74973306/126264948-22c6beca-59e6-485b-ba6b-b4bfa299b948.png)


Write a query to find the node type of Binary Tree ordered by the value of the node. Output one of the following for each node:

- Root: If node is root node.
- Leaf: If node is leaf node.
- Inner: If node is neither root nor leaf node.


---

- 내 풀이

```sql
SET @a := 0;

SELECT @a := @a + 1, IF(
    @a = (
        SELECT n
        FROM BST
        WHERE p is NULL
        ), 'Root',IF(
            @a IN (
                SELECT distinct p
                FROM BST
                ), 'Inner', 'Leaf'
    ))
                        
FROM BST
```


- 다른 사람 풀이

```sql
SELECT CASE
	WHEN P IS NULL THEN CONCAT(N, ' Root')
	WHEN N IN (SELECT DISTINCT P FROM BST) THEN CONCAT(N, ' Inner')
	ELSE CONCAT(N, ' Leaf')
	END
FROM BST
ORDER BY N ASC
```
