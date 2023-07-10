
{ lib, pkgs, config, modulesPath,
	lf, zsh, oh-my-zsh, home-manager
,	 ... }:

with lib;
let
  nixos-wsl = import ./nixos-wsl;

  autosuggest_pluginPath = "./use/zsh-autosuggestions";
  ohmyzshPluginDir = "${pkgs.oh-my-zsh}/share/oh-my-zsh/custom/plugins";

  # Home Manager
# for unstable 
#  home-manager = builtins.fetchTarball "https://github.com/nix-community/home-manager/archive/master.tar.gz";
  home-manager = builtins.fetchTarball "https://github.com/nix-community/home-manager/archive/release-22.05.tar.gz";
in
{
  imports = [
    "${modulesPath}/profiles/minimal.nix"
#      ./hardware-configuration.nix
    nixos-wsl.nixosModules.wsl
#    ./use/zsh-autosuggestions
#    (import "${home-manager}/nixos")
<home-manager/nixos>
#    ./home.nix
#  <home-manager/nixos>
  ];

  wsl = {
    enable = true;
    automountPath = "/mnt";
    defaultUser = "magic";
    startMenuLaunchers = true;

    # Enable native Docker support
    # docker-native.enable = true;

    # Enable integration with Docker Desktop (needs to be installed)
    # docker-desktop.enable = true;

  };


	
  # Enable nix flakes
  #nix.package = pkgs.nixFlakes;
  #nix.extraOptions = ''
  #  experimental-features = nix-command flakes
  #'';

  system.stateVersion = "22.05";

#  shellHook = ''
#    cp -r ${autosuggest_pluginPath} ${ohmyzshPluginDir}/zsh-autosuggestions
#  '';

  nixpkgs.config.allowUnfree = true;

#environment.systemPackages = [pkgs.git
#  # Other system packages
#  pkgs.neofetch
#	pkgs.htop
#	pkgs.wget
#	pkgs.curl
#];


  # installed packages
  environment.systemPackages = with pkgs; [
    # cli utils
    git
    curl
    wget
    vim
    htop
    neovim
	neofetch
	pfetch
	cmatrix
	python3	
 ];

  users.users.magic = {
    isNormalUser  = true;
    home  = "/home/magic";
    description  = "Magic is happening";
    extraGroups  = [ "wheel" "networkmanager" ];
	shell = pkgs.zsh;
	# packages = with pkgs; [git];
	};


	programs.zsh = {
	 # ... # Your zsh config
	#ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE="fg=#00FFFF,";
	#alias p=python3.7;
	#enable = true;
	enable = false;
	 ohMyZsh = {
	    enable = true;
	    plugins = [  "git" ]; #"zsh-autosuggestions"]; #"thefuck" ];
	#    theme = "robbyrussell";
	  };


	};
	
	programs.zsh.promptInit = ""; # Clear this to avoid a conflict with oh-my-zsh

        environment.interactiveShellInit = ''
          alias gs='git status'
          alias switch='sudo nixos-rebuild switch'
          ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE="fg=#00FFFF,"
          alias p=python3.7
#	cd ~
        '';
	 programs.zsh.interactiveShellInit = ''
#	cd ~ #
	cmatrix -C yellow -s	
	export PATH=$HOME/bin:/usr/local/bin:$PATH
	echo "ZSH! NIXOS"
#	 cp -r ${autosuggest_pluginPath} ${ohmyzshPluginDir}/zsh-autosuggestions
#	  echo !!! ${pkgs.oh-my-zsh}
	  export ZSH=${pkgs.oh-my-zsh}/share/oh-my-zsh/
	
	  # Customize your oh-my-zsh options here
	  ZSH_THEME="robbyrussell"	  
	  # ZSH_THEME="agnoster"
	 # plugins=(git zsh-autosuggestions )
	plugins=(git)
 #         ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE="fg=#00FFFF,"
	  source $ZSH/oh-my-zsh.sh
#	  neofetch
	  '';

  # Enable Home Manager
home-manager.useGlobalPkgs = true;
home-manager.users.magic = { pkgs, ... }: {
  home.packages = [ pkgs.wget pkgs.zsh pkgs.oh-my-zsh] ; # zsh ]; # wget ]; # oh-my-zsh];
  home.username = "magic";
  home.homeDirectory = "/home/magic";
  programs.home-manager.enable = true;

  
  home.stateVersion = "22.05";


# programs.zsh.enable = true;
 programs.zsh = {
#  ... # Your zsh config
enable = true;
#environment.interactiveShellInit = ''
#initExtra = "echo @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@";
    #sessionVariables = {
    #    EDITOR = "kaka";
    #	ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE="fg=#FF00FF,";
    #};
initExtra = ''
        alias switch='sudo nixos-rebuild switch'
	export PATH=$HOME/bin:/usr/local/bin:$PATH
        echo "ZSH!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!! HOME MANAGER"
        # cp -r ${autosuggest_pluginPath} ${ohmyzshPluginDir}/zsh-autosuggestions
        #  echo !!! ${pkgs.oh-my-zsh}
          export ZSH=${pkgs.oh-my-zsh}/share/oh-my-zsh/

          # Customize your oh-my-zsh options here
          ZSH_THEME="robbyrussell"
          # ZSH_THEME="agnoster"
          #plugins=(git zsh-autosuggestions )
	#${pkgs.oh-my-zsh}/share/oh-my-zsh/
          #ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE="fg=#FF00FF," # purple
          ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE="fg=#00FFFF," # cyan
          setopt PROMPT_SUBST
        # ORG_PS1      = "%(?:%{%}➜ :%{%}➜ ) %{$fg[cyan]%}%c%{$reset_color%} $(git_prompt_info)"
        # color test = %(?:%{%}%{$fg[green]%}➜%{$reset_color%} :%{%}{$fg[red]%}➜%{$reset_color%} )
        export PS1="%(?:%{%}➜xxxmag :%{%}➜yyymag ) %{$fg[cyan]%}%n@%M%{$reset_color%} %{$fg[cyan]%}%c%{$reset_color%} $(git_prompt_info)"
	  export RPROMPT='%*'
	  source $ZSH/oh-my-zsh.sh
	  export PROMPT="%(?:%{%}%{$fg[green]%}➜%{$reset_color%} :%{%}%{$fg[red]%}➜%{$reset_color%} ) %{$fg[yellow]%}%n$reset_color%}%{$fg[magenta]%}@$reset_color%}%{$fg[pink]%}%M%{$reset_color%} %{$fg[cyan]%}%0~%{$reset_color%} $(git_prompt_info)"	
	cmatrix -C magenta -s && neofetch
	echo "Your system is ready."
	echo ""

          '';
#programs.zsh = {
#enable = true;
oh-my-zsh = {
    enable = true;
    plugins = [ "git" ]; # "thefuck" ];
    theme = "robbyrussell";
  };
plugins = [
    {
      # will source zsh-autosuggestions.plugin.zsh
      name = "zsh-autosuggestions";
      src = pkgs.fetchFromGitHub {
        owner = "zsh-users";
        repo = "zsh-autosuggestions";
        rev = "v0.4.0";
        sha256 = "0z6i9wjjklb4lvr7zjhbphibsyx51psv50gm07mbb0kj9058j6kc";
      };
    }
    {
      name = "enhancd";
      file = "init.sh";
      src = pkgs.fetchFromGitHub {
        owner = "b4b4r07";
        repo = "enhancd";
        rev = "v2.2.1";
        sha256 = "0iqa9j09fwm6nj5rpip87x3hnvbbz9w9ajgm6wkrd5fls8fn8i5g";
      };
    }
  ];
};


};





#ROOT USER#####################################
###############################################
home-manager.users.root = { pkgs, ... }: {
  home.packages = [ pkgs.wget pkgs.zsh pkgs.oh-my-zsh pkgs.pfetch] ; # zsh ]; # wget ]; # oh-my-zsh];
#  home.username = "root";
#  home.homeDirectory = "/home/root";
  programs.home-manager.enable = true;

  
  home.stateVersion = "22.05";


# programs.zsh.enable = true;
 programs.zsh = {
#  ... # Your zsh config
enable = true;
#environment.interactiveShellInit = ''
#initExtra = "echo @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@";
    #sessionVariables = {
    #    EDITOR = "kaka";
    #	ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE="fg=#FF00FF,";
    #};
initExtra = ''
	alias switch='sudo nixos-rebuild switch'
        export PATH=$HOME/bin:/usr/local/bin:$PATH
        echo "ZSH!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!! HOME MANAGER ROOT"
        # cp -r ${autosuggest_pluginPath} ${ohmyzshPluginDir}/zsh-autosuggestions
        #  echo !!! ${pkgs.oh-my-zsh}
          export ZSH=${pkgs.oh-my-zsh}/share/oh-my-zsh/

          # Customize your oh-my-zsh options here
          ZSH_THEME="robbyrussell"
          # ZSH_THEME="agnoster"
          #plugins=(git zsh-autosuggestions )
	#${pkgs.oh-my-zsh}/share/oh-my-zsh/
          ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE="fg=#FF00FF," # purple
         # ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE="fg=#00FFFF," # cyan
	setopt PROMPT_SUBST
	# ORG_PS1      = "%(?:%{%}➜ :%{%}➜ ) %{$fg[cyan]%}%c%{$reset_color%} $(git_prompt_info)"
	# color test = %(?:%{%}%{$fg[green]%}➜%{$reset_color%} :%{%}{$fg[red]%}➜%{$reset_color%} ) 
#        export PS1="%(?:%{%}➜xxx :%{%}➜yyy ) %{$fg[cyan]%}%n@%M%{$reset_color%} %{$fg[cyan]%}%c%{$reset_color%} $(git_prompt_info)"
	export RPROMPT='%*'
	  source $ZSH/oh-my-zsh.sh
 #       export PS1="%(?:%{%}➜xxx1 :%{%}➜yyy1 ) %{$fg[cyan]%}%n@%M%{$reset_color%} %{$fg[cyan]%}%c%{$reset_color%} $(git_prompt_info)"
        export PROMPT="%(?:%{%}%{$fg[green]%}➜%{$reset_color%} :%{%}%{$fg[red]%}➜%{$reset_color%} ) %{$fg[red]%}%n$reset_color%}%{$fg[magenta]%}@$reset_color%}%{$fg[pink]%}%M%{$reset_color%} %{$fg[cyan]%}%0~%{$reset_color%} $(git_prompt_info)"
          cmatrix -C yellow -s && pfetch
	echo "Your system is ready. Logged in as root  %{$fg[red]%}%n{$reset_color%}"
	echo ""

          '';
#programs.zsh = {
#enable = true;
oh-my-zsh = {
    enable = true;
    plugins = [ "git" ]; # "thefuck" ];
    theme = "robbyrussell";
  };
plugins = [
    {
      # will source zsh-autosuggestions.plugin.zsh
      name = "zsh-autosuggestions";
      src = pkgs.fetchFromGitHub {
        owner = "zsh-users";
        repo = "zsh-autosuggestions";
        rev = "v0.4.0";
        sha256 = "0z6i9wjjklb4lvr7zjhbphibsyx51psv50gm07mbb0kj9058j6kc";
      };
    }
    {
      name = "enhancd";
      file = "init.sh";
      src = pkgs.fetchFromGitHub {
        owner = "b4b4r07";
        repo = "enhancd";
        rev = "v2.2.1";
        sha256 = "0iqa9j09fwm6nj5rpip87x3hnvbbz9w9ajgm6wkrd5fls8fn8i5g";
      };
    }
  ];
};


};

##################################################
##################################################

  # Enable Home Manager
# home-manager.users.magic = {
#    enable = true;
#    home.stateVersion = "22.05";
#  };

  # Enable nix flakes
  nix.package = pkgs.nixFlakes;
  nix.extraOptions = ''
    experimental-features = nix-command flakes
  '';


  
}
