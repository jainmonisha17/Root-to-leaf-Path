# Root-to-leaf-Path
Return all root to leaf paths
// Problem 2: Given a binary tree, return all root-to-leaf paths.

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
