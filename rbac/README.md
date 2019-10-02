Role-based access control (RBAC) is a method of regulating access to
computer or network resources based on the roles of individual users
within an enterprise.

RBAC api objects include:
Pods
PersistentVolumes
ConfigMaps
Deployments
Nodes
Secrets
Namespaces

Possible operations that can be performed on above resources:
create
get
delete
list
update
edit
view
watch
exec


To manage RBAC in Kubernetes, apart from resources and operations, we need the following elements:

Rules: A rule is a set of operations (verbs) that can be carried out
on a group of resources which belong to different API Groups.

Roles and ClusterRoles: Both consist of rules. The difference between
a Role and a ClusterRole is the scope: in a Role, the rules are applicable
to a single namespace, whereas a ClusterRole is cluster-wide, so the rules
are applicable to more than one namespace. ClusterRoles can define rules
for cluster-scoped resources (such as nodes) as well. Both Roles and
ClusterRoles are mapped as API Resources inside our cluster.

Subjects: These correspond to the entity that attempts an operation in
the cluster. There are three types of subjects:

User Accounts: These are global, and meant for humans or processes living
outside the cluster. There is no associated resource API Object in the Kubernetes cluster.
Service Accounts: This kind of account is namespaced and meant for intra-cluster
processes running inside pods, which want to authenticate against the API.
Groups: This is used for referring to multiple accounts. There are some groups
created by default such as cluster-admin (explained in later sections).
RoleBindings and ClusterRoleBindings: Just as the names imply, these bind subjects
to roles (i.e. the operations a given user can perform). As for Roles and
ClusterRoles, the difference lies in the scope: a RoleBinding will make the
rules effective inside a namespace, whereas a ClusterRoleBinding will make the
rules effective in all namespaces.


Reference: https://kubernetes.io/docs/reference/access-authn-authz/rbac/