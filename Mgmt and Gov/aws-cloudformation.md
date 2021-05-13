# AWS Cloudformation

Stacks
You can assign a service role, if you can iam:PassRole it. Anyone who can operate on that stack can leverage that role's permissions (even if they can't run it - they could modify it then someone else runs it!).
Otherwise the user/role that is using the stack needs to have permission to perform all the operations
StackSets
Custom administration role, with identity policies that constrain iam:PassRole for that role to control who can use it
Custom execution role, with limits on what resources it has action to, and a trust policy for specific administration role(s) in the admin account
Some interesting condition keys:
cloudformation:ChangeSetName e.g. enforce prefixes
cloudformation:ResourceTypes to control which resources can be involved in a stack
cloudformation:TemplateUrl e.g. can only create stacks from this URL (as oppoed to operating on an existing stack resource)
