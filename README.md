# BST-
#include<stdio.h>
#include<stdlib.h>
struct node
{
    int data;
    struct node*left_child;
    struct node*right_child;
};
struct node*newnode(int x)
{
    struct node*p;
    p=malloc(sizeof(struct node));
    p->data=x;
    p->left_child=NULL;
    p->right_child=NULL;
    return p;
}
struct node*insert(struct node*root,int x)
{
    if(root==NULL)
    return newnode(x);
    else if(x>root->data)
    root->right_child=insert(root->right_child,x);
    else
    root->left_child=insert(root->left_child,x);
    return root;
}
void inorder(struct node*root)
{
    if(root!=NULL)
    {
        inorder(root->left_child);
        printf("%d",root->data);
        inorder(root->right_child);
    }
}
void preorder(struct node*root)
{
    if(root!=NULL)
    {
        printf("%d",root->data);
        preorder(root->left_child);
        preorder(root->right_child);
    }
}
void postorder(struct node*root)
{
    if(root!=NULL)
    {
        postorder(root->left_child);
        postorder(root->right_child);
        printf("%d",root->data);
    }
}
struct node*search(struct node*root,int x)
{
    if(root==NULL||root->data==x)
    return root;
    else if(x>root->data)
    return search(root->right_child,x);
    else
    return search(root->left_child,x);
}
struct node*find_min(struct node*root)
{
    if(root==NULL)
    return NULL;
    else if(root->left_child!=NULL)
    return find_min(root->left_child);
    return root;
}
struct node*delete(struct node*root,int x)
{
    if(root==NULL)
    return NULL;
    else if(x>root->data)
    {
    root->right_child=delete(root->right_child,x);
    }
    else if(x<root->data)
    {
    root->left_child=delete(root->left_child,x);
    }
    else
    {
        if(root->left_child==NULL&&root->right_child==NULL)
        {
            free(root);
            return NULL;
        }
            else if(root->left_child||root->right_child==NULL)
            {
                struct node*temp;
                if(root->left_child==NULL)
                {
                temp=root->right_child;
                }
                else
                {
                temp=root->left_child;
                free(root);
                }
                return temp;
            }
            
            else
            {
                struct node*temp=find_min(root->right_child);
                root->data=temp->data;
                root->right_child=delete(root->right_child,temp->data);
            }
        
        return root;
    }
}
int main()
{
    struct node*root;
    root=newnode(20);
    insert(root,8);
    insert(root,1);
    insert(root,15);
    insert(root,9);
    insert(root,12);
    insert(root,30);
    printf("the inorder is:\n");
    inorder(root);
    printf("the preorder is:\n");
    preorder(root);
    printf("the postorder is:\n");
    postorder(root);
    printf("\n");
    root=delete(root,1);
    root=delete(root,30);
    root=delete(root,9);
    printf("inorder after deletion is:\n");
    inorder(root);
    printf("preorder after deletion is:\n");
    preorder(root);
    printf("postorder after deleteion is:\n");
    postorder(root);
    printf("\n");
    return 0;
}
