[\[GIT\] - 02. GIT으로 버전 관리하기](https://rina214.tistory.com/3)

## 브랜치란?

모든 버전 관리 시스템에는 '브랜치(Branch)'라는 개념이 있습니다. 나무가 가지에서 새 줄기를 뻗듯이 여러 갈래로 퍼지는 데이터 흐름을 가리키는 말입니다.

### 브랜치 기능

 깃으로 버전 관리를 시작하면 기본적으로 master라는 브랜치가 만들어집니다. 사용자가 커밋할 때마다 master 브랜치는 최신 커밋을 가리킵니다. 여기서 새 브랜치를 만들면 기존에 저장한 파일을 master 브랜치에 그대로 유지하면서 기존파일 내용을 수정하거나 새로운 기능을 구현할 파일을 만들 수 있습니다. 이렇게 master 브랜치에서 뻗어 나오는 새 브랜치를 만드는 것을 '분기(branch)한다'고 합니다. 그리고 새 브랜치에서 원하는 작업을 다 끝냈다면 새 브랜치에 있던 파일을 원래  master 브랜치에 합치는 것을 '병합(merge)한다'고 합니다. 

---

## 브랜치 만들기

 01. 터미널 창을 열어 홈 디렉터리에 manual이라는 새 디렉터리를 만들고 해당 디렉터리로 이동합니다.

  mkdir manual

  cd manual

02\. manual 디렉터리를 저장소로 만들고 .git 디렉터리가 만들어졌는지 확인해 보세요.

  git init

  ls -al

03\. manual 디렉터리 안에 work.txt 파일을 만들어 'content 1'이라는 내용을 입력한 다음 저장하세요.

  vim work.txt

04\. work.txt파일을 스테이지에 올리고 커밋합니다. 커밋 메시지는 간단히 'work 1'이라고 하겠습니다.

  git add work.txt

  git commit -m "work 1"

05\. 커밋이 완료되면 다음과 같이 입력해서 커밋 내역을 확인해 보세요.

  git log

[##_Image|kage@Z8Smh/btqBBffMM45/IKgIKhGDK3uwgBu3vHTTck/img.png|alignCenter|data-origin-width="0" data-origin-height="0" width="498" height="506"|||_##]

06\. work.txt 파일을 두 번 더 커밋해 보겠습니다. work.txt 파일에 'content 2'를 추가한 후 'work 2'라는 메시지와 함께 커밋하고, 또 파일 내용에 'content 3'를 추가한 후 'work 3'라는 메시지와 함께 커밋합니다.

  vim work.txt

  git commit -am "work 2"

  vim work.txt

  git commit -am "work 3"

07\. 커밋이 끝나면 커밋 내역을 확인해 보세요.

  git log

[##_Image|kage@Ltpog/btqBxzUkMz5/HPNtddKtLrbNOuFFTABFx0/img.png|alignCenter|data-origin-width="0" data-origin-height="0" width="565" height="589"|||_##]

 master 브랜치가 가장 최신 커밋인 'work 3'를 가리키고 있고, HEAD가 master 브랜치를 가리키고 있습니다. HEAD는 여러 브랜치 중에서 현재 작업 중인 브랜치를 가리킵니다.

### 1\. 새 브랜치 만들기

01\. 깃에서 브랜치를 만들거나 확인하는 명령은 git branch입니다.

  git branch

 master라고 나타날텐데 master는 특별한 브랜치입니다. 저장소를 만들 때 기본적으로 master 브랜치가 만들어집니다. 우리는 그동안 master 브랜치에서 작업하고 있었던 것이죠.

02\. 새로운 브랜치를 만들려면 git branch 명령 다음에 만들려는 브랜치 이름을 적습니다. 

  git branch google

03\. 현재 저장소의 브랜치를 확인하기 위해 다음과 같이 입력해 봅시다.

  git branch

 master 앞에 \* 표시는 아직 우리가 master 브랜치에서 작업하고 있다는 뜻입니다.

04\. 브랜치가 추가된 후에는 커밋 로그 화면도 다르게 나타납니다.

  git log

 커밋 로그를 확인하면 (HEAD -> master, google)이라고 되어있습니다. 이 표시는 저장소에 master, google 2개의 브랜치가 있고, HEAD -> master이므로 현재 작업 중인 브랜치는 master 브랜치라는 의미입니다.

05\. 같은 방법으로 apple 브랜치와 ms 브랜치를 만들어 보세요. 그리고 git branch 명령으로 저장소 안에 있는 모든 브랜치를 확인해 보세요.

  git branch apple

  git branch ms

  git branch

[##_Image|kage@Ruj7A/btqBxz06dX2/yW6UAGESm0ePXskqWwKkP0/img.png|alignCenter|data-origin-width="0" data-origin-height="0" width="542" height="621"|새 브랜치 만들기||_##]

### 2\. 브랜치 사이 이동하기

  현재 우리는 master 브랜치에 있습니다.

01\. work.txt 파일 안에 'master content 4'라는 내용을 추가한 후 'master work 4'라는 메시지와 함께 커밋해 보겠습니다.

  vim work.txt

  git commit -am "master work 4"

02\. git log 명령에 --oneline 옵션을 추가해서 확인해 보겠습니다. --oneline 옵션은 한 줄에 한 커밋씩 나타내 주기 때문에 커밋을 간략히 확인할 때 편리합니다.

  git log --oneline

 최신 커밋인 'master work 4'는 master 브랜치에만 적용되어 있음을 알 수 있습니다.

03\. 다른 브랜치로 이동하려면 git checkout 명령 다음에 브랜치 이름을 사용합니다.

  git checkout google

 $ 위에 나타난 파일 경로 끝에 (google)이라고 표시될 것입니다. 현재 브랜치가 google이라는 뜻입니다.

04\. 작업 브랜치를 google 브랜치로 바꿨을 때 어떤 변화가 생기는지 확인해 보겠습니다. 

  git log --oneline

05\. google 브랜치의 최신 커밋은 'work 3' 커밋입니다. work.txt 파일에는 무엇이 있을지 확인해 보겠습니다.

  cat work.txt

 'content 1'에서 'content 3'까지의 내용만 있고 'master content 4'가 없습니다. 이를 통해 google 브랜치가 master 브랜치에서 분기된 이후에 master 브랜치에 추가된 커밋은 google 브랜치에 영향을 미치지 않았단 것을 알 수 있습니다.

[##_Image|kage@b9PxPC/btqBBglt493/3FB53WuViY0SXGYoPZkrf1/img.png|alignCenter|data-origin-width="0" data-origin-height="0" width="504" height="431"|브랜치 사이 이동하기||_##]

---

## 브랜치 정보 확인하기

### 1\. 새 브랜치에서 커밋하기

 현재 브랜치는 google일 겁니다.

01\. google 브랜치에는 work.txt 파일이 있습니다. 빔에서 파일을 열고 'google content 4'라는 텍스트를 추가하고 저장합니다.

  vim work.txt

02\. google.txt 파일을 만들고 'google content 4'라는 텍스트를 입력한 후 저장합니다.

  vim google.txt

03\. 수정된 2개의 파일을 각각 스테이지에 올릴 수도 있지만 git add 뒤에 마침표(.)를 추가하면 현재 저장소에서 수정된 파일을 한꺼번에 스테이지에 올릴 수 있습니다. 그리고 'google content 4'라는 메시지와 함께 커밋합니다.

  git add .

  git commit -m "google content 4"

04\. git log 명령을 사용할 때 다음과 같이 --branches 옵션을 사용하면 각 브랜치의 커밋을 함께 볼 수 있습니다.

  git log --oneline --branches

 (HEAD -> google)이라고 되어 있으니 현재 google 브랜치에 체크아웃한 상태이고, google 브랜치의 최신 커밋은 'google content 4'입니다. 그리고 master 브랜치의 최신 커밋은 'master content 4', ms 브랜치와 apple 브랜치의 최신 커밋은 'work 3'입니다.

05\. 브랜치와 커밋의 관계를 좀 더 보기 쉽게 그래프 형태로 표시하려면 git log 명령에 --graph 옵션을 함께 사용합니다.

  git log --oneline --branches --graph

 커밋 내역 왼쪽에 수직선(|, /)이 커밋과 커밋의 관계를 보여주는 것입니다. 브랜치 앞의 \*과 이어진 수직선을 확인하면 됩니다. 'work 3' 커밋까지는 google 브랜치와 master 브랜치의 부모 커밋이 같고, 그 이후부터 다른 커밋을 만들었다는 사실을 알 수 있습니다.

### 2\. 브랜치 사이의 차이점 알아보기

 브랜치마다 커밋이 쌓여갈수록 브랜치 사이에 어떤 차이가 있는지 일일이 확인하기 어려워집니다. 이럴 때 브랜치 이름 사이에 마침표 두 개(..)를 넣은 명령으로 차이점을 쉽게 확인할 수 있습니다.

  git log master..google

이렇게 하면 master 브랜치에는 없고 google 브랜치에만 있는 커밋만 보여줍니다.

  git log google..master

반대로 google 브랜치를 기준으로 master를 비교하면 master 브랜치에만 있는 'master content 4' 커밋을 보여줍니다. 

[##_Image|kage@bK6Cru/btqBzPoCfaI/VGZ5nWthyzs7PTTEwblXdk/img.png|alignCenter|data-origin-width="0" data-origin-height="0" width="552" height="710"|브랜치 정보 확인하기||_##]

---

## 브랜치 병합하기

 만들어진 각 브랜치에서 작업을 하다가 어느 시점에서는 브랜치 작업을 마무리하고 기존 브랜치와 합해야 합니다. 이것을 '브랜치 병합(merge)'이라고 합니다. 

### 1\. 서로 다른 파일 병합하기

 브랜치 병합은 처음에 공부하기 까다롭기 때문에 새로운 저장소를 만들어서 필요한 브랜치와 커밋만 사용해 연습해 보겠습니다.

01\. 홈 디렉터리로 이동해 manual-2라는 깃 저장소를 만들텐데, git init 다음에 디렉터리 이름을 입력하면 새로운 디렉터리를 만들고 저장소를 초기화하는 과정을 한꺼번에 처리할 수 있습니다.

  cd ~

  git init manual-2

  cd manual-2

  ls -al

02\. 우선 work.txt 파일을 만듭니다. 그리고 o2라는 브랜치를 만듭니다. 현재는 master 브랜치에 있는 상황에서 master.txt라는 파일을 만들고 'master work 2'라는 메시지와 함께 커밋합니다. 이제 o2 브랜치로 체크아웃한 뒤 o2.txt 파일을 만들고 'o2 work 2'라는 메시지와 함께 커밋합니다. 커밋의 상태를 확인해보았을 때 다음과 같이 나오면 잘하신겁니다.

[##_Image|kage@SQ7r7/btqByG6KuC9/Pecj4lg6oHbYRktTfrqbDK/img.png|alignCenter|data-origin-width="0" data-origin-height="0" width="557" height="809"|||_##]

03\. o2 브랜치에서 작업이 다 끝났다고 가정하고, o2 브랜치의 내용을 master 브랜치로 병합해 보겠습니다. 브랜치를 병합하려면 먼저 master 브랜치로 체크아웃해야 합니다.

  git checkout master

04\. 브랜치를 병합하려면 git merge 명령 뒤에 가져올 브랜치 이름을 적습니다.

  git merge o2

 자동으로 빔이 실행되면서 'Merge branch o2'라는 커밋메시지가 나타납니다. 브랜치를 병합하면서 만들어지는 커밋의 메시지입니다. 커밋 메시지를 수정할 수도 있고, 자동 메시지를 그대로 사용해도 됩니다. Esc키를 누르고 ':wq'를 입력해 내용을 저장한 후 편집기를 종료합니다. 

05\. ls -al 명령을 사용해 확인해 보면 o2 브랜치에 있던 o2.txt 파일이 master 브랜치에 합쳐져있을 것입니다.

  ls -al

06\. 브랜치와 커밋들이 어떻게 병합되었는지 확인하면 'o2 work 2' 커밋이 master 브랜치에 병합되면서 'Merge branch o2'라는 커밋이 새로 생겼습니다. 

  git log --oneline --branches --graph

[##_Image|kage@bdKE5A/btqBuQvxfWg/KYcEaObIyL7rggBcxjqcX1/img.png|alignCenter|data-origin-width="0" data-origin-height="0" width="435" height="435"|서로 다른 파일 병합하기||_##]

두 브랜치에서 서로 다른 파일을 병합하는 경우 이렇게 깃에서 간단히 해결할 수 있습니다.

> **브랜치를 병합할 때 편집기 창이 열리지 않게 하려면**  
>  앞에서 브랜치를 병합할 때 자동으로 편집기가 실행되면서 커밋 메시지를 추가 작성할 수 있었습니다. 만약 편집기 창을 열지 않고 깃에서 지정하는 커밋 메시지를 그대로 사용하겠다면 다음과 같이 --no-edit 옵션을 추가합니다.  
>   git merge o2 --no-edit  
> 브랜치를 병합할 때 편집기 창이 나타나지 않도록 설정한 경우, 커밋 메시지를 추가하거나 수정하고 싶다면 병합 명령에 --edit 옵션을 사용합니다.  
>   git merge o2 --edit

### 2\. 같은 문서의 다른 위치를 수정했을 때 병합하기

01\. 홈 디렉터리로 이동한 후 manual-3라는 깃 저장소를 만들고, manual-3 디렉터리로 이동합니다.

  cd ~

  git init manual-3

  cd manual-3

02\. 빔에서 work.txt 파일을 만들고 다음과 같이 입력합니다. 나중에 work.txt 문서를 수정하고 병합할 것이기 때문에 내용 사이에 두 줄의 공백을 두었습니다.

  vim work.txt

> #title  
> content  
>   
>   
> #title  
> content

03\. 방금 만든 work.txt를 스테이지에 올리고 커밋합니다. 커밋 메시지는 'work 1'이라고 하겠습니다. 그 다음 o2라는 새로운 브랜치를 만듭니다. master 브랜치와 o2 브랜치에는 모두 'work 1'커밋이 있게 됩니다. master 브랜치의 work.txt를 다음과 같이 수정합니다.

> #title  
> content  
> master content 2  
>   
> #title  
> content

수정한 work.txt를 'master work 2'라는 커밋 메시지와 함께 커밋하세요. 그리고 o2 브랜치로 체크아웃하고 o2 브랜치의 work.txt 파일도 수정하겠습니다.

> #title  
> content  
>   
>   
> #title  
> content  
> o2 content 2

수정한 work.txt 파일을 커밋해 보세요. 커밋 메시지는 'o2 work 2'라고 하겠습니다.

04\. 양쪽 브랜치에서 work.txt 파일을 수정했지만 문서 안의 수정 위치는 다릅니다. 이럴 경우 어떻게 해야할까요? o2 브랜치를 master 브랜치에 합치기 위해 master 브랜치로 체크아웃합니다.

  git checkout master

05\. git merge 명령을 사용해 o2 브랜치를 master 브랜치로 끌어옵니다.

  git merge o2

 원하는 커밋메시지를 작성한 다음 저장하고 편집기를 종료합니다.

06\. cat 명령을 사용해 work.txt 파일을 확인해보세요. master 브랜치의 수정 내용과 o2 브랜치의 수정 내용이 자연스럽게 하나의 파일에 합쳐진 것을 볼 수 있습니다. 이렇게 자동으로 합쳐주는 기능이 있어 깃은 더욱 강력한 도구가 됩니다.

[##_Image|kage@bXv1u9/btqBAEmSJ6n/1W8qXb4ioQh0VK6c9JKKw0/img.png|alignCenter|data-origin-width="0" data-origin-height="0" width="549" height="827"|같은 문서의 다른 위치를 수정했을 때 병합하기||_##]

### 3\. 같은 문서의 같은 위치를 수정했을 때 병합하기

 깃에서는 줄 단위로 변경 여부를 확인합니다. 그래서 각 브랜치에 같은 파일 이름을 가지고 있으면서 같은 줄을 수정했을 때 브랜치를 병합하면 브랜치 충돌(conflict)이 발생합니다.

01\. 홈 디렉터리로 이동한 후 manual-4라는 깃 저장소를 만들고, manual-4 디렉터리로 이동합니다.

  cd ~

  git init manual-4

  cd manual-4

02\. 빔에서 work.txt 파일을 만들고 다음과 같이 입력합니다. 나중에 work.txt 문서의 같은 위치를 수정하기 위해 두 내용 사이에 빈 줄을 하나만 두었습니다.

> #title  
> content  
>   
> #title  
> content

03\. 방금 만든 work.txt를 스테이지에 올리고 커밋합니다. 이제 o2라는 브랜치를 만듭니다. 현재 브랜치 master인 상태에서 work.txt를 수정하겠습니다.

> #title  
> content  
> master content 2  
> #title  
> content

수정한 work.txt를 커밋하고 o2 브랜치로 체크아웃하여 work.txt 파일을 수정합니다.

> #title  
> content  
> o2 content 2  
> #title  
> content

수정한 work.txt 파일을 커밋해 보세요.

04\. master 브랜치로 체크아웃한 후 o2 브랜치를 master 브랜치로 끌어옵니다.

  git checkout master

  git merge o2

 이번엔 자동으로 빔이 열리지 않고 메시지가 나타납니다. 이 메시지는 work.txt를 자동 병합하는 동안 충돌(conflict)이 발생했다는 뜻입니다.

[##_Image|kage@nRLS5/btqBBfNFASO/eXz2P70hKErrApWDVB0Bzk/img.png|alignCenter|data-origin-width="0" data-origin-height="0" width="577" height="821"|||_##]

05\. 충돌이 생긴 문서는 자동으로 병합될 수 없으므로 사용자가 직접 충돌 부분을 해결한 후 커밋해야 합니다.

  vim work.txt

06\. '<<<<<<< HEAD'와 가운데 가로줄(=======) 사이의 내용은 현재(master) 브랜치에서 수정한 내용입니다. 그리고 가로줄(=======)과 '>>>>>>> o2' 사이의 내용은 o2 브랜치에서 수정한 내용입니다. 양쪽 브랜치의 내용을 참고하면서 직접 내용을 수정해야 합니다. 내용을 원하는 대로 수정했으면 '<<<<<<< HEAD'나 '>>>>>>> o2', 가로줄(=======)은 삭제하고 저장한 후 편집기를 종료합니다.

07\. 이제 수정한 work.txt를 스테이지에 올리고 커밋하면 됩니다. 커밋 메시지는 'merge o2 branch'로 하겠습니다.

  git commit -am "merge o2 branch"

08. git log --oneline --branches --graph를 통해 지금까지 만든 브랜치와 커밋의 관계를 확인해 보세요.

[##_Image|kage@baZj59/btqBuvZrg3p/rDEzQkYgNNiebKHCtKY6ik/img.png|alignCenter|data-origin-width="0" data-origin-height="0" width="431" height="194"|||_##]

### 4\. 병합이 끝난 브랜치 삭제하기

 브랜치를 병합한 후 더 이상 사용하지 않는 브랜치는 깃에서 삭제할 수 있습니다. 단, 이렇게 브랜치를 삭제하더라도 이 브랜치가 완전히 지워지는 것이 아니라 다시 같은 이름의 브랜치를 만들면 예전 내용을 다시 볼 수 있습니다.

01\. git branch 명령을 사용하면 현재 저장소에 어떤 브랜치가 있는지 확인할 수 있습니다.

  git branch

02\. 저장소의 기본 브랜치는 master이므로 브랜치를 삭제하려면 master 브랜치에서 해야 합니다. 

  git checkout master

03\. 브랜치를 삭제할 때는 git branch 명령에 -d 옵션을 사용합니다.

  git branch -d o2

[##_Image|kage@bflqMg/btqBuQCjhUE/nfs53TFWJy1xaVzq8ex4UK/img.png|alignCenter|data-origin-width="0" data-origin-height="0" width="369" height="130"|브랜치 삭제하기||_##]

---

## 브랜치 관리하기

### 1\. 브랜치에서 checkout과 reset의 작동 원리

[02장](https://rina214.tistory.com/3)에서 이미 checkout 명령과 reset 명령을 공부했습니다. 하지만 브랜치와 함께라면 더 다양하게 사용할 수 있습니다.

01\. test라는 깃 저장소를 만들고, test 디렉터리로 이동합니다.

  git init test

  cd test

02\. 빔에서 c1.txt파일을 만들고 스테이지에 올린 후 커밋합니다. 커밋 메시지는 c1이라고 하겠습니다.

  vim c1.txt

  git add c1.txt

  git commit -m "c1"

03\. git log 명령을 실행합니다.

  git log --oneline

(HEAD -> master) 표시가 있습니다. HEAD는 현재 작업 트리(working directory)가 어떤 버전을 기반으로 작업 중인지를 가리키는 포인터입니다. HEAD는 기본적으로 master를 가리키고 브랜치에 담긴 커밋 중에서 가장 최근의 커밋을 가리킵니다.

04\. 이제 sub라는 브랜치를 만들겠습니다.

  git branch sub

05\. 빔에서 c2.txt 파일을 만들고 스테이지에 올린 후 'c2'라는 메시지와 함께 커밋합니다.

  vim c2.txt

  git add c2.txt

  git commit -m "c2"

 master는 c2 커밋을 가리키고, HEAD는 그대로 master 브랜치를 가리킵니다.

06\. master 브랜치에서 sub 브랜치로 이동합니다.

  git checkout sub

 이제 HEAD는 sub 브랜치를 가리키게 됩니다. 

07\. sub 브랜치에서 s1.txt 문서를 만들고 's1'이라는 메시지와 함께 커밋하세요. 

  vim s1.txt

  git add s1.txt

  git commit -m "s1"

 이제 HEAD는 sub 브랜치를 가리키고 sub는 s1 커밋을 가리키고 있습니다.

08\. [02장](https://rina214.tistory.com/3)에서는 reset 명령으로 master 브랜치에 있던 여러 커밋 중 하나를 골라서 되돌아갔습니다. 브랜치가 여러 개일 때는 현재 브랜치가 아닌 다른 브랜치에 있는 커밋을 골라서 최신 커밋으로 지정할 수 있습니다. 예를 들어 sub 브랜치에 있는 상태에서 master 브랜치에 있는 c2 커밋을 sub 브랜치의 최신 커밋으로 지정해보겠습니다. 먼저 c2커밋의 커밋 해시를 확인합니다.

  git log --oneline --branches

09\. git reset 명령 다음에 c2 커밋의 커밋 해시를 입력합니다.

  git reset 커밋 해시

10\. git log --oneline --branches --graph 명령을 사용해 확인하면 sub 브랜치의 최신 커밋이 c2로 바뀌고 HEAD는 그대로 sub 브랜치를 가리키고 있습니다. 그리고 sub 브랜치는 c2 커밋을 가리키고 있기 때문에 원래 가리키고 있던 s1 커밋은 연결이 끊기면서 삭제됩니다.

11\. git checkout 명령을 사용하면 HEAD를 제어해서 브랜치를 이동할 수 있습니다.

 git reset 명령을 사용하면 HEAD가 가리키고 있는 브랜치의 최신 커밋을 원하는 커밋으로 지정할 수 있습니다. 이때 어떤 브랜치에 있는 커밋이든 지정할 수 있으며, 명령을 수행한 뒤 브랜치와 연결이 끊긴 커밋은 삭제됩니다.

[##_Image|kage@bgkx5C/btqByFtjYor/8e92v6O07ZlMwyrErcQiYK/img.png|alignCenter|data-origin-width="0" data-origin-height="0" width="541" height="751"|||_##]

### 2\. 수정 중인 파일 감추기 및 되돌리기

 브랜치에서 파일을 수정하고 커밋하지 않은 상태에서 급하게 다른 파일을 커밋해야 할 경우가 있습니다. 아직 커밋하지 않은 파일들을 그냥 두어도 상관없지만 계속 커밋하라는 메시지가 나타나기 때문에 번거롭습니다. 실수로 다른 파일과 함께 커밋이 될 수도 있고요.

01\. st라는 저장소를 만들고 st 디렉터리로 이동합니다.

  git init st

  cd st

02. git stash 명령을 사용하려면 파일이 tracked 상태여야 합니다. 즉 한 번은 커밋한 상태여야 하죠. 빔을 사용해 f1.txt 파일을 작성한 후 스테이지에 올리고, 'f1'이라는 메시지와 함께 커밋합니다.

  vim f1.txt

  git add f1.txt

  git commit -m "f1"

03\. f2.txt 파일도 'f2'라는 메시지와 함께 커밋합니다.

  vim f2.txt

  git add f2.txt

  git commit -m "f2"

04\. 빔에서 f1.txt 파일을 연 후 내용을 수정하고 저장합니다. f2.txt 파일도 수정하고 저장합니다.

  vim f1.txt

  vim f2.txt

05\. git status 명령을 실행해 보면 현재 브랜치에서 f1.txt와 f2.txt가 수정되었다고 나타납니다.

  git status 

06\. 커밋하지 않은 수정 내용을 어딘가에 보관하려면 git stash 명령을 사용합니다. git stash save 또는 간단히 git stash라고만 해도 됩니다.

  git stash

07\. 다시 한번 git status 명령을 실행해보면 modified 메시지가 사라진 것을 알 수 있습니다.

  git status

08\. 이렇게 감춘 파일들은 stasg 목록에서 확인할 수 있습니다. 가장 먼저 감춘 것은 stash@{0}에 들어있는데, 앞으로 다른 파일이 추가되면 기존 파일은 stash@{1}로 옮겨지고 새로 추가된 파일은 stash@{0}에 담깁니다. 즉 가장 최근에 보관한 것이 stash@{0}에 담깁니다.

  git stash list

09\. 급한 작업을 모두 마쳤다면 감춰둔 파일을 꺼내와 계속 수정하거나 커밋할 수 있습니다. git stash 명령 뒤에 pop를 추가하면 stash 목록에서 가장 최근 항목을 되돌립니다.

git stash pop

[##_Image|kage@bb2rCn/btqBxAyXv59/KO8N1ZWxC1wEIMw74Kw1v0/img.png|alignCenter|data-origin-width="0" data-origin-height="0" width="551" height="648"|git stash||_##]
