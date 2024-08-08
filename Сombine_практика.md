# InterviewKit_1

## конвертировать из closure’оф в combine
Дана схема на UIKit + Delegate где вся логика во вью контроллере. Задача - перенести логику из контроллера в ViewModel (MVVM) + Сделать общение через Combine.

```
protocol LoginViewDelegate {
    func didChangeUsernameField(_ text: String)
    func didChangePasswordField(_ text: String)
    func continueButtonTapped()
}

class LoginView: UIView {
    private let usernameTextField = UITextField()
    private let passwordTextField = UITextField()
    private let continueButton = UIButton()
    var delegate: LoginViewDelegate?
    
    func setup() {
        self.addSubview(usernameTextField)
        self.addSubview(passwordTextField)
        self.addSubview(continueButton)
    }
}

class LoginViewController: UIViewController {
    private let contentView = LoginView()
    private let requestManager: LoginRequestManager

    init(requestManager: LoginRequestManager) {
         self.requestManager = requestManager
         self.init(nibName: nil, bundle: nil)
    }

    required init?(coder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }

    override init(nibName: String?, bundle: Bundle?) {
        super.init(nibName: nibName, bundle: bundle)
    }

    override func viewDidLoad() {
        super.viewDidLoad()
        setup()
    }

    func setup() {
        contentView.setup()
        contentView.delegate = self
    }
}


extension LoginViewController: LoginViewDelegate {
    func didChangeUsernameField(_ text: String) {
        // Проверяет на уникальность username
        requestManager.checkUsername(text) { result in
            switch result {
                case success(let isValid):
                    if !isSafe {
                        self.continueButton.isEnabled = false
                    } else {
                        self.continueButton.isEnabled = true
                    }
                case failure(let error):
                    print(error.localizedDescription)
            }
        }
    }

    func didChangePasswordField(_ text: String) {
        // Проверяет на надежность пароля
        requestManager.checkPassword(text) { result in
            switch result {
                case success(let isSafe):
                    if !isSafe {
                        self.continueButton.isEnabled = false
                    } else {
                        self.continueButton.isEnabled = true
                    }
                case failure(let error):
                    print(error.localizedDescription)
            }
        }
    }

    func continueButtonTapped() {
        requestManager.login() { result in
            switch result {
                case success(let isLoginSuccessful):
                    // Отображает Alert юзеру
                case failure(let error):
                    print(error.localizedDescription)
            }
        }
    }
}
```
