# Pathogen
Plugin 관리를 위해 default로 .vim/bundle 경로에 있는 plugin을 로드하도록 runtime path를 조작(?)하는 플러그인.
http://www.vim.org/ 에는 현재 보이지 않는데 [pathogen 저장소][pathogen-repo]를 참고해서 설치함.
```bash
mkdir -p ~/.vim/autoload ~/.vim/bundle
curl -LSso ~/.vim/autoload/pathogen.vim https://tpo.pe/pathogen.vim
```
설치 후 ~/.vim/.vimrc 파일 생성해서 아래 내용을 추가
```bash
execute pathogen#infect()
syntax on
filetype plugin indent on
```
[Dracula vim theme][dracula-vim-theme] 페이지를 확인해서 아래 command로 theme 추가
```bash
cd ~/.vim
git submodule add git@github.com:dracula/vim.git bundle/dracula-theme
```
Submodule로 추가된 theme 정보까지 해서 [dotvim 저장소][mydotvim-repo]를 생성함.
다른 장비에서도 dotvim clone만 해서 사용하면 될 것으로 생각됨.

[pathogen-repo]: https://github.com/tpope/vim-pathogen
[mydotvim-repo]: https://github.com/blurblah/dotvim
[dracula-vim-theme]: https://draculatheme.com/vim/