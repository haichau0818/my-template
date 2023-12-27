// Css:

/* CSS Register page*/

.wrapper{
    background: #ececec;
    padding: 0 20px 0 20px
}
.register{
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
}
.row{
    width: 900px;
    height: 600px;
    border-radius: 10px;
    background: #fff;
    box-shadow: 5px 5px 10px 1px rgba(0,0,0,0.3)
}
.register-side-image {
    background-image: url("/images/plott.png");
    background-position: center;
    background-size: cover;
    background-repeat: no-repeat;
    position: relative;
    border-radius: 10px 0 0 10px;
}
.register-side-image img{
    width: 100px;
    position: absolute;
    top: -200px;
    left: -60px;
}
.text{
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%,-50%);
}
.text p{
    color: #fff;
    font-size:20px;
}
.text i{
    font-weight:400;
    font-size : 20px;
}
.right{
    display: flex;
    justify-content: center;
    align-items: center;
    position:relative;
}

.input-box{
    width: 330px;
    box-sizing: border-box;
}
.input-box header{
    font-weight: 700;
    font-size:24px;
    text-align: center;
    margin-bottom: 45px;
}
.input-field{
    display: flex;
    flex-direction: column;
    position: relative;
    padding: 0 10px 0 10px;
}

.input{
    height: 45px;
    width:100%;
    background: transparent;
    border: none;
    border-bottom: 1px solid rgba(0,0,0,0.3);
    outline: none;
    margin-bottom: 20px;
    color: #40414a;
}
.input-box .input-field label{
    position:absolute;
    top:10px;
    left:10px;
    pointer-events: none;
    transition: .5s;
}

.input-field .input:focus ~ label{
    top: -10px;
    font-size:13px;
}
.input-field .input:valid ~ label {
    top: -10px;
    font-size: 13px;
    color: #5d5076;
}
.input-field .input:focus, .input-field .input:valid {
    border-bottom: 1px solid #743ae1;
}
.submit{
    border: none;
    outline: none;
    height: 45px;
    background: #ececec;
    border-radius: 5px;
    transition: .5s;
}

.submit:hover{
    background: rgba(34,4,3,0.4);
    color: #fff;
}
.signin{
    text-align: center;
    font-size:small;
    margin-top:20px;
}

span a {
    text-decoration: none;
    font-weight: 700;
    color: #3BC3FF;
    transition:.5s;
}
    span a:hover {
        text-decoration: underline;
        color: #3BC3FF;
    }


---------------------------
@layout EmtyLayout

@page "/register"

<div class="container register">
    <div class="row">
        <div class="col-md-6 register-side-image">
            <div class="text">
                <img class="register-image" src="/images/logo_cyllenge_cl.svg" alt="img"/>
                <p>Create account chat<i> - Plott</i></p>
            </div>
        </div>
        <div class="col-md-6 right">
            <EditForm Model="myModel" OnSubmit="Registration">
            <div class="input-box">
                <header>Create account</header>
                <div class="input-field">
                    <input type="text" class="input" id="fullName" required autocomplete="off" />
                    <label for="fullName">Full name</label>
                </div>
                 <div class="input-field">
                    <input type="text" class="input" id="username" required autocomplete="off" />
                    <label for="username">Username</label>
                </div>
                 <div class="input-field">
                    <input type="text" class="input" id="email" required autocomplete="off" />
                    <label for="email" >Email</label>
                </div>
                <div class="input-field">
                    <input type="password" class="input" id="password" required />
                    <label for="password">Password</label>
                </div>
                <div class="input-field">
                    <input type="password" class="input" id="confirmPassword" required/>
                    <label for="confirmPassword">Confirm Password</label>
                </div>
                <div class="input-field">
                    <input type="submit" class="submit" value="Sign Up"/>
                </div>
                <div class="signin">
                    <span>Already have an account!<a href="login">Login here</a></span>
                </div>
            </div>
            </EditForm>
        </div>
    </div>
</div>

--------layout


@inherits LayoutComponentBase

<div class="wrapper">@Body</div>
