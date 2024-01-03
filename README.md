# Root-to-leaf-Path
Return all root to leaf paths
// Problem 2: Given a binary tree, return all root-to-leaf paths.


               12     Sum: 23

                                                         7              1

                                                  4            10            5


                                                                 12     

                                                         7              1      Sum: 11

                                                  4            10            5


                                                  
                                                                 12     

                                                         7              1        

                                                  4            10            5      Sum: 4 
Time Complexity The time complexity of the above algorithm is , where ‘N’ is the total number of nodes in the tree. This is due to the fact that we traverse each node once (which will take O(N)), and for every leaf node, we might have to store its path (by making a copy of the current path) which will take O(N).

We can calculate a tighter time complexity of from the space complexity discussion below.

Space Complexity If we ignore the space required for the allPaths list, the space complexity of the above algorithm will be O(N) in the worst case. This space will be used to store the recursion stack. The worst-case will happen when the given tree is a linked list (i.e., every node has only one child).

How can we estimate the space used for the allPaths array? Take the example of the following balanced tree:

Image Here we have seven nodes (i.e., N = 7). Since, for binary trees, there exists only one path to reach any leaf node, we can easily say that total root-to-leaf paths in a binary tree can’t be more than the number of leaves. As we know that there can’t be more than leaves in a binary tree, therefore the maximum number of elements in allPaths will be (N + 1) / 2. Now, each of these paths can have many nodes in them. For a balanced binary tree (like above), each leaf node will be at maximum depth. As we know that the depth (or height) of a balanced binary tree is O(logN) we can say that, at the most, each path can have logN nodes in it. This means that the total size of the allPaths list will be O(N * log N). If the tree is not balanced, we will still have the same worst-case space complexity.

From the above discussion, we can conclude that our algorithm’s overall space complexity is O(N * log N).

Also, from the above discussion, since for each leaf node, in the worst case, we have to copy log(N) nodes to store its path; therefore, the time complexity of our algorithm will also be O(N * log N).

                                                  Sum: 23 - 12 = 11
                                                  Sum: 11 - 7 = 4
                                                  Sum: 4 - 4 = 0

                                                  Tree paths with sum 23: [[12, 7, 4], [12, 1, 10]]


import java.util.*;

public class allRootToLeafPathssum {

    static class TreeNode {
        int val;
        TreeNode left;
        TreeNode right;

        TreeNode(int x) {
            val = x;
        }
    }

    public List<List<Integer>> findPaths(TreeNode root, int sum) {
        List<List<Integer>> allPaths = new ArrayList<>();
        List<Integer> currentPath = new ArrayList<>();

        findRec(root, currentPath, allPaths);
        return allPaths;
    }

    public static void findRec(TreeNode currentNode, List<Integer> currentPath, List<List<Integer>> allPaths) {
        if (currentNode == null)
            return;

        currentPath.add(currentNode.val);

        if (currentNode.left == null && currentNode.right == null) {
            allPaths.add(new ArrayList<Integer>(currentPath));
        }

        findRec(currentNode.left, currentPath, allPaths);
        findRec(currentNode.right, currentPath, allPaths);

    }

    currentPath.remove(currentPath.size()-1);

}

    public static void main(String[] args) {
        allRootToLeafPathssum sol = new allRootToLeafPathssum();
        TreeNode root = new TreeNode(12);
        root.left = new TreeNode(7);
        root.right = new TreeNode(1);
        root.left.left = new TreeNode(4);
        root.right.left = new TreeNode(10);
        root.right.right = new TreeNode(5);
        int sum = 23;
        List<List<Integer>> result = sol.findPaths(root, sum);
        System.out.println("Tree paths with sum " + sum + ": " + result);
    }
}
