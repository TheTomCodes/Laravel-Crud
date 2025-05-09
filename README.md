Crude_Oprations:https://github.com/siddharth018/laravel-8-image-crud
login_and_register:https://github.com/bhuvaneshcj/laravel-custom-registration-and-login.git
```
public function register(Request $request)
{
    $this->validate($request, [
        'name' => 'required',
        'email' => 'required|email|unique:users',
        'password' => 'required|min:8',
    ]);

    $user = new User();
    $user->name = $request->name;
    $user->email = $request->email;
    $user->password = \Hash::make($request->password);
    $user->save();

    toastr()->success('Registration successful! Please login.');
    return redirect('login'); // Go to login page after registration
}
```

```
public function login(Request $request)
{
    $this->validate($request, [
        'email' => 'required|email',
        'password' => 'required|min:8',
    ]);

    $credentials = $request->only('email', 'password');

    if (Auth::attempt($credentials)) {
        return redirect('/'); // Redirect to homepage/index after login
    }

    toastr()->error('Invalid email or password');
    return redirect('login');
}
```
