# TODO: Simplify Sign-In/Sign-Up and Admin User Management

## Backend Changes
- [x] Fix authController.js: Complete signIn function, remove role param from signUp and signIn, default new users to 'user' role.
- [x] Add getAllUsers function in adminController.js to fetch all users.
- [x] Add updateUserRole function in adminController.js for admins to change user roles.
- [x] Update adminRoute.js: Add routes for getAllUsers and updateUserRole.

## Frontend Changes
- [x] Update SignUp.jsx: Remove role dropdown, default to user.
- [x] Update SignIn.jsx: Remove role dropdown.
- [x] Update AllUsers.jsx: Fetch users, display in table with role columns, add buttons to promote/demote roles.

## Testing
- [ ] Test sign-up: Should create user role by default.
- [ ] Test sign-in: Should log in based on stored role.
- [ ] Check admin panel: View all users, change roles.
