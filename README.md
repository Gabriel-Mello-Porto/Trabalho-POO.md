# Trabalho-POO

## backfield.java
```java
import java.awt.*;
import javax.swing.*;

class ImagePanel extends JPanel {
    private Image image;
    private int x, y;

    public ImagePanel(Image image, int x, int y) {
        this.image = image;
        this.x = x;
        this.y = y;
        setPreferredSize(new Dimension(x, y));
    }

     @Override
        protected void paintComponent(Graphics g) {
            super.paintComponent(g);
            // Imagem de fundo
            g.drawImage(image, 0, 0, getWidth(), getHeight(), this);
        }
}
```

## backgroundimg.java
```java
import java.awt.*;
import javax.swing.*;

class backgroundimg extends JPanel {
    private Image backgroundImage;

    
    public backgroundimg(String imagePath) {
        backgroundImage = new ImageIcon("imgs/Coverart2.png").getImage();
    }

    @Override
    protected void paintComponent(Graphics g) {
        super.paintComponent(g);
        // Draw the background image
        g.drawImage(backgroundImage, 0, 0, getWidth(), getHeight(), this);
    }
}
```

## changebackground.java
```java
import java.awt.*;
import javax.swing.*;

class changebackground extends JPanel {
    private Image backgroundImage;


    public changebackground(String imagePath) {
        backgroundImage = new ImageIcon("imgs/Upgradescreen2.png").getImage();
    }

    @Override
    protected void paintComponent(Graphics g) {
        super.paintComponent(g);
        // Imagem de fundo
        g.drawImage(backgroundImage, 0, 0, getWidth(), getHeight(), this);
    }
}
```

## Chefao.java
```java
import javax.swing.ImageIcon;

public class Chefao extends Inimigo {

    ImageIcon portrait = new ImageIcon("imgs/Billy.png");

    Chefao(String nome, int hp, int atk, int def) {
        super(nome, hp, atk, def);
    }

    public ImageIcon getPortrait() {
        return portrait;
    }
}
```



## ChScreen.java
```java
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

class ChScreen extends JFrame implements ActionListener {

    // botões
    private JButton hpp;
    private JButton hpm;

    private JButton atkp;
    private JButton atkm;

    private JButton defp;
    private JButton defm;

    private JButton Bconfirm;

    private JLabel heroname;
    private JLabel infohp;
    private JLabel infoatk;
    private JLabel infodef;
    private JLabel pointsLabel;

    private ImageIcon picture;

    private Hero character;

    private boolean escolhaModoJogo;

    public int points = 10;

    public ChScreen(Hero character, boolean escolhaModoJogo) {
        super("Customização de Personagem");
        this.character = character;
        this.escolhaModoJogo = escolhaModoJogo;

        // icone de janela
        ImageIcon icon = new ImageIcon("imgs/WWC2icon.png");
        setIconImage(icon.getImage());

        Container tela = getContentPane();
        setSize(800, 480);
        setLayout(new BorderLayout());
        setLocationRelativeTo(null);

        changebackground backimg = new changebackground("imgs/Upgradescreen2.png");
        backimg.setLayout(null);

        Dimension buttonSize = new Dimension(80, 30);

        // inicialização
        hpp = new JButton("HP+");
        hpp.setSize(buttonSize);

        hpm = new JButton("HP-");
        hpm.setSize(buttonSize);

        atkp = new JButton("ATK+");
        atkp.setSize(buttonSize);

        atkm = new JButton("ATK-");
        atkm.setSize(buttonSize);

        defp = new JButton("DEF+");
        defp.setSize(buttonSize);

        defm = new JButton("DEF-");
        defm.setSize(buttonSize);

        Bconfirm = new JButton("Confirm");
        Bconfirm.setSize(100, 30);

        // listeners
        hpp.addActionListener(this);
        hpm.addActionListener(this);
        atkp.addActionListener(this);
        atkm.addActionListener(this);
        defp.addActionListener(this);
        defm.addActionListener(this);
        Bconfirm.addActionListener(this);

        // labels
        String name = character.getClass().getSimpleName();
        heroname = new JLabel("" + name);
        heroname.setForeground(Color.BLACK);

        infohp = new JLabel("HP: " + character.getHp(), SwingConstants.CENTER);
        infohp.setForeground(Color.BLACK);

        infoatk = new JLabel("ATK: " + character.getAtk(), SwingConstants.CENTER);
        infoatk.setForeground(Color.BLACK);

        infodef = new JLabel("DEF: " + character.getDef(), SwingConstants.CENTER);
        infodef.setForeground(Color.BLACK);

        pointsLabel = new JLabel("Points Left: " + points, SwingConstants.CENTER);
        pointsLabel.setForeground(Color.BLACK);

        // imagem de personagem
        picture = scaleImageIcon(character);
        JLabel Lportrait = new JLabel(picture);
        // posição e tamanho da imagem
        Lportrait.setBounds(446, 90, 200, 200);

        // painel de botões
        JPanel buttonPanel = new JPanel(new GridLayout(4, 2, 20, 20));
        buttonPanel.setOpaque(false);
        buttonPanel.setBounds(60, 80, 250, 300);

        // Adding buttons and labels to the button panel
        buttonPanel.add(hpm);
        buttonPanel.add(infohp);
        buttonPanel.add(hpp);

        buttonPanel.add(atkm);
        buttonPanel.add(infoatk);
        buttonPanel.add(atkp);

        buttonPanel.add(defm);
        buttonPanel.add(infodef);
        buttonPanel.add(defp);

        // posição do confirm
        Bconfirm.setBounds(140, 380, 100, 30);
        // posição dos labels
        pointsLabel.setBounds(60, 300, 250, 30);
        heroname.setBounds(146, 55, 250, 30);

        // adicionando elementos na tela
        backimg.add(buttonPanel);
        backimg.add(Bconfirm);
        backimg.add(Lportrait);
        backimg.add(pointsLabel);
        backimg.add(heroname);

        // imagem de fundo
        tela.add(backimg, BorderLayout.CENTER);

        setVisible(true);
    }

    @Override
    public void actionPerformed(ActionEvent action) {
        if (action.getSource() == hpp && points > 0) {
            character.setHp(character.getHp() + 1);
            points--;
        } else if (action.getSource() == hpm) {
            if (character.getHp() > character.getbaseHp()) {
                character.setHp(character.getHp() - 1);
                points++;
            }
        } else if (action.getSource() == atkp && points > 0) {
            character.setAtk(character.getAtk() + 1);
            points--;
        } else if (action.getSource() == atkm) {
            if (character.getAtk() > character.getbaseAtk()) {
                character.setAtk(character.getAtk() - 1);
                points++;
            }
        } else if (action.getSource() == defp && points > 0) {
            character.setDef(character.getDef() + 1);
            points--;
        } else if (action.getSource() == defm) {
            if (character.getDef() > character.getbaseDef()) {
                character.setDef(character.getDef() - 1);
                points++;
            }
        } else if (action.getSource() == Bconfirm) {
            // Opens the battlefield screen
            new Field(character, escolhaModoJogo);
            dispose();
        }
        updater();
    }


    private void updater() {
        infohp.setText("HP: " + character.getHp());
        infoatk.setText("ATK: " + character.getAtk());
        infodef.setText("DEF: " + character.getDef());
        pointsLabel.setText("Points Left: " + points);
    }

    private ImageIcon scaleImageIcon(Hero chara) {
        ImageIcon imgbuf = new ImageIcon(chara.getPortrait().getImage());
        Image img = imgbuf.getImage();
        Image scaledImg = img.getScaledInstance(200, 200, Image.SCALE_SMOOTH);
        return new ImageIcon(scaledImg);
    }
}
```

## Field.java
```java
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;
import javax.swing.border.*;
import java.io.File;
import java.io.IOException;
import java.util.Random;
import java.util.ArrayList;

class Field extends JFrame implements ActionListener, KeyListener {

    private JPanel battlefield;

    private Hero heroi;

    private ImageIcon picture, Wpicture;;

    private Image battleground_img, wooden_img;
    
    private JLabel infohp;
    private JLabel infoatk;
    private JLabel infodef;
    private JLabel inventinfo;

    private JButton N_game;
    private JButton Reiniciar;
    private JButton botaoVisibilidade;

    private Font custom;
    private boolean visibilidade;

    //====================battleinfo========================

    JButton[] botoes = new JButton[50];
    Random aleatorio = new Random();
    JButton botaoDica = new JButton();
    int limiteUsosDica = 3;
    int hpAntesBatalhas;
    int atkAntesBatalhas;
    int defAntesBatalhas;
    
    // Posicoes
    int posicaoHeroi = aleatorio.nextInt(9);  // Posicao do heroi aleatoria da linha inicial
    int posicaoAnteriorHeroi = posicaoHeroi;  // Posicao anterior e para caso heroi fuja do combate
    int posicaoChefao = aleatorio.nextInt(40, 49);  // Posicao do chefao aleatoria da linha final

    // Criacao de vetores para posicoes e inimigos
    ArrayList<Inimigo> vetorInimigos = new ArrayList<Inimigo>();
    ArrayList<Integer> posicoesInimigos = new ArrayList<Integer>();
    ArrayList<Integer> posicoesArmadilhasLeves = new ArrayList<Integer>();
    ArrayList<Integer> posicoesArmadilhasPesadas = new ArrayList<Integer>();
    ArrayList<Integer> posicoesWhiskey = new ArrayList<Integer>();    

    // Criacao de vetores para armazenar as posicoes iniciais (botao resetar)
    private int posicaoInicialHeroi = posicaoHeroi;
    private int posicaoInicialChefao = posicaoChefao;

    ArrayList<Inimigo> vetorInimigosIniciais = new ArrayList<Inimigo>();
    
    private ArrayList<Integer> posicoesInimigosIniciais = new ArrayList<>();
    private ArrayList<Integer> posicoesArmadilhasLevesIniciais = new ArrayList<>();
    private ArrayList<Integer> posicoesArmadilhasPesadasIniciais = new ArrayList<>();
    private ArrayList<Integer> posicoesWhiskeyIniciais = new ArrayList<>();

    // Imagens
    ImageIcon heroiIcon;
    ImageIcon indioIcon;
    ImageIcon rogueIcon;
    ImageIcon billyIcon;
    ImageIcon armadilhaPesadaIcon;
    ImageIcon armadilhaLeveIcon;
    ImageIcon whiskeyIcon;

    //=============================================================================================
    public Field(Hero heroi, boolean visibilidade) {
        super("Battlefield");
        this.heroi = heroi;
        this.visibilidade = visibilidade;

        // Tratando imagens
        heroiIcon = heroi.getPortrait();
        indioIcon = new ImageIcon("imgs\\Indio.png");
        rogueIcon = new ImageIcon("imgs\\Rogue.png");
        billyIcon = new ImageIcon("imgs\\Billy.png");
        armadilhaPesadaIcon = new ImageIcon("imgs\\Beartrap.png");
        armadilhaLeveIcon = new ImageIcon("imgs\\Cactus.png");
        whiskeyIcon = new ImageIcon("imgs\\whiskey.png");    

        // Valida o caminho imagens
        try {
            verificarImagem(heroiIcon);
            verificarImagem(indioIcon);
            verificarImagem(rogueIcon);
            verificarImagem(billyIcon);
            verificarImagem(armadilhaPesadaIcon);
            verificarImagem(armadilhaLeveIcon);
            verificarImagem(whiskeyIcon);

        } catch (IOException e) {
            System.out.println(e.getMessage());
        }
        
        // icone de janela
        ImageIcon icon = new ImageIcon("imgs/WWC2icon.png");
        setIconImage(icon.getImage());

        // resolução e icone
        setSize(1280, 758);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(null);
        setLocationRelativeTo(null);

        // ============================Painel de fundo=============================

        // carregar imagem de personagem
        picture = scaleImageIconHero(heroi, 200, 200);
        JLabel Lportrait = new JLabel(picture);
        Lportrait.setBounds(1030, 30, 200, 200);

        // label de info de personagem
        infohp = new JLabel("HP: " + heroi.getHp(), SwingConstants.CENTER);
        infohp.setForeground(Color.BLACK);

        infoatk = new JLabel("ATK: " + heroi.getAtk(), SwingConstants.CENTER);
        infoatk.setForeground(Color.BLACK);

        infodef = new JLabel("DEF: " + heroi.getDef(), SwingConstants.CENTER);
        infodef.setForeground(Color.BLACK);

        JPanel infodisplay = new JPanel(new GridLayout(3, 1, 0, 2));
        infodisplay.setOpaque(false);
        infodisplay.setBounds(1030, 210, 200, 200);

        infodisplay.add(infohp);
        infodisplay.add(infoatk);
        infodisplay.add(infodef);

        // criando label de inventario
        JLabel Invent = new JLabel("Inventario");
        Invent.setBounds(1090, 450, 100, 20);
        Invent.setForeground(Color.BLACK);
        inventinfo = new JLabel("X: " + heroi.getNumWhiskey());
        inventinfo.setBounds(1140, 490, 100, 100);
        inventinfo.setForeground(Color.BLACK);

        // Label de itens do inventario
        Wpicture = new ImageIcon("imgs/whiskey.png");
        Wpicture = scaleImageIcon(Wpicture, 100, 100);
        JLabel Wportrait = new JLabel(Wpicture);
        Wportrait.setBounds(1030, 480, 100, 100);

        // carregando fundos
        battleground_img = new ImageIcon("imgs/Fieldsml.png").getImage();
        wooden_img = new ImageIcon("imgs/depth2.png").getImage();

        // painel de madeira
        JPanel Woodenpanel = new ImagePanel(wooden_img, 1280, 720);
        Woodenpanel.setBounds(0, 0, 1280, 720);
        Woodenpanel.setLayout(null);
        this.setLocationRelativeTo(null);

        // painel de combate
        battlefield = new ImagePanel(battleground_img, 1000, 650);
        battlefield.setBounds(0, 0, 1000, 650);
        battlefield.setBorder(BorderFactory.createLineBorder(Color.BLACK, 2));
        battlefield.setLayout(new GridLayout(5, 10));
        battlefield.addKeyListener(this);
        battlefield.setFocusable(true);       

        // Instancia 50 botoes adicionando ao frame e o ActionListener
        for (int i = 0; i < 50; i++) {
            botoes[i] = new JButton();
            botoes[i].addActionListener(this);
            battlefield.add(botoes[i]);

            // Deixa os botoes invisiveis (para colocar uma imagem de fundo)
            botoes[i].setOpaque(false);
            botoes[i].setContentAreaFilled(false);
            botoes[i].setBorderPainted(false);
        }

        // Painel de botões inferiores
        N_game = new JButton("Novo Jogo");
        Reiniciar = new JButton("Reiniciar");
        botaoDica = new JButton("Dica");
        botaoVisibilidade = new JButton("Alternar Visibilidade");

        N_game.setOpaque(false);
        Reiniciar.setOpaque(false);
        botaoDica.setOpaque(false);
        botaoVisibilidade.setOpaque(false);

        botaoDica.addActionListener(this);
        N_game.addActionListener(this);
        Reiniciar.addActionListener(this);
        botaoVisibilidade.addActionListener(this);

        JPanel painel_fundo = new JPanel(new FlowLayout(FlowLayout.CENTER));
        painel_fundo.add(N_game);
        painel_fundo.add(Reiniciar);
        painel_fundo.add(botaoDica);
        painel_fundo.add(botaoVisibilidade);
        painel_fundo.setBounds(80, 660, 800, 30);
        painel_fundo.setOpaque(false);

        // colocando um painel no outro
        Woodenpanel.add(battlefield);
        Woodenpanel.add(Lportrait);
        Woodenpanel.add(infodisplay);
        Woodenpanel.add(Invent);
        Woodenpanel.add(inventinfo);
        Woodenpanel.add(Wportrait);
        Woodenpanel.add(painel_fundo);

        // adicionando os paineis na tela
        add(Woodenpanel);
        setVisible(true);

        // Escala as imagens
        int escalaX = 105;
        int escalaY = 105;
        armadilhaPesadaIcon = scaleImageIcon(armadilhaPesadaIcon, escalaX, escalaY);
        armadilhaLeveIcon = scaleImageIcon(armadilhaLeveIcon, escalaX, escalaY);
        whiskeyIcon = scaleImageIcon(whiskeyIcon, escalaX, escalaY);
        indioIcon = scaleImageIcon(indioIcon, escalaX, escalaY);
        rogueIcon = scaleImageIcon(rogueIcon, escalaX, escalaY);
        billyIcon = scaleImageIcon(billyIcon, escalaX, escalaY);
        heroiIcon = scaleImageIcon(heroiIcon, escalaX, escalaY);
        
        // Posiciona heroi e chefao
        botoes[posicaoHeroi].setIcon(heroiIcon); // Define a imagem do heroi no botao
        botoes[posicaoChefao].setIcon(billyIcon); // Define a imagem do chefao no botao

        // Cria e distribui inimigos e armadilhas pelo campo
        distribuirArmadilhasPesadas(3);
        distribuirArmadilhasLeves(3);
        distribuirIndios(3);
        distribuirRogues(3);
        distribuirWhiskey(4);

        hpAntesBatalhas = heroi.getHp();
        atkAntesBatalhas = heroi.getAtk();
        defAntesBatalhas = heroi.getDef();
            
    }

    @Override
    public void actionPerformed(ActionEvent e) {

        // Dica
        if (e.getSource() == botaoDica) {
            if (limiteUsosDica == 0){
                JOptionPane.showMessageDialog(this, "Limite de dicas alcancado!");
                battlefield.requestFocusInWindow(); // Atualiza o foco para o teclado, assim pode usar setas novamente apos clicar em um botao
            }else {                
                if (verificarArmadilhasAoRedor()) {
                    limiteUsosDica--;
                    JOptionPane.showMessageDialog(this, "Tem no minimo uma armadilha ao seu redor\n                    Tome cuidado");
                    battlefield.requestFocusInWindow(); // Atualiza o foco para o teclado, assim pode usar setas novamente apos clicar em um botao
                } else {
                    limiteUsosDica--;
                    JOptionPane.showMessageDialog(this, "Nenhuma armadilha encontrada ao seu redor!");
                    battlefield.requestFocusInWindow(); // Atualiza o foco para o teclado, assim pode usar setas novamente apos clicar em um botao
                }
            }
        }

        if (e.getSource() == Reiniciar) {
            reiniciarJogo();
            battlefield.requestFocusInWindow(); // Atualiza o foco para o teclado, assim pode usar setas novamente apos clicar em um botao
        }

        // Muda visibilidade
        if (e.getSource() == botaoVisibilidade) {
            if (!visibilidade) {
                mudarVisibilidade(true);
                visibilidade = true;
                battlefield.requestFocusInWindow(); // Atualiza o foco para o teclado, assim pode usar setas novamente apos clicar em um botao
            } else {
                mudarVisibilidade(false);
                visibilidade = false;
                battlefield.requestFocusInWindow(); // Atualiza o foco para o teclado, assim pode usar setas novamente apos clicar em um botao
            }    
        }

        if (e.getSource() == N_game) {
            JOptionPane.showMessageDialog(this, "Iniciando novo jogo");
            new Mwindows();
            dispose();
        }

        // Nao utilizado no momento (provavelmente deletar para o projeto final) (so usei para ajudar com as logicas do programa)
        for (int i = 0; i < 50; i++) {
            if (e.getSource() == botoes[i]) {
                System.out.println("Botao " + i + " pressionado");
                battlefield.requestFocusInWindow();
            }
        }
    }

    private boolean verificarArmadilhasAoRedor() {
        int[] direcoes = {-1, 1, -10, 10, -9, 9, -11, 11};  // Direcoes a verificar
        int[] posicoesSemParedeEsquerda = {1, -10, 10, -9, 11};  // Direcoes a verificar
        int[] posicoesSemParedeDireita = {-1, -10, 10, 9, -11};  // Direcoes a verificar
        int posicaoVerificarAtual;

        // Heroi esta na primeira coluna
        if (posicaoHeroi % 10 == 0) {
            for (int i = 0; i < posicoesSemParedeEsquerda.length; i++) {

                posicaoVerificarAtual = posicaoHeroi + posicoesSemParedeEsquerda[i];

                // Nao verificar alem do 'teto' ou do 'chao' do campo de batalha
                if (posicaoVerificarAtual >= 0 && posicaoVerificarAtual < 50) {
                    if (posicoesArmadilhasLeves.contains(posicaoVerificarAtual) || posicoesArmadilhasPesadas.contains(posicaoVerificarAtual)) {
                        return true;  
                    }
                }

            }
        }

        // Heroi esta na ultima coluna
        else if (posicaoHeroi % 10 == 9) {      
            for (int i = 0; i < posicoesSemParedeDireita.length; i++) {

                posicaoVerificarAtual = posicaoHeroi + posicoesSemParedeDireita[i];

                // Nao verificar alem do 'teto' ou do 'chao' do campo de batalha
                if (posicaoVerificarAtual >= 0 && posicaoVerificarAtual < 50) {
                    if (posicoesArmadilhasLeves.contains(posicaoVerificarAtual) || posicoesArmadilhasPesadas.contains(posicaoVerificarAtual)) {
                        return true;  
                    }
                }

            }
        }

        // Heroi esta em qualquer outra coluna
        else {
            for (int i = 0; i < direcoes.length; i++) {
                
                posicaoVerificarAtual = posicaoHeroi + direcoes[i];

                // Nao verificar alem do 'teto' ou do 'chao' do campo de batalha
                if (posicaoVerificarAtual >= 0 && posicaoVerificarAtual < 50) {
                    if (posicoesArmadilhasLeves.contains(posicaoVerificarAtual) || posicoesArmadilhasPesadas.contains(posicaoVerificarAtual)) {
                        return true;  
                    }
                }
            }
        }    
        return false; 
    }
    
    private boolean posicaoNaoEstaLivre(int posicao){
        // Garante que os inimigos nao fiquem na mesma posicao que o heroi ou entre si, nem com as armdilhas
        if (posicao == posicaoHeroi || posicao == posicaoChefao || posicoesInimigos.contains(posicao) || posicoesArmadilhasLeves.contains(posicao) || posicoesArmadilhasPesadas.contains(posicao) || posicoesWhiskey.contains(posicao)) {
            return true;
        }return false;
    }

    private void distribuirWhiskey(int numWhiskey) {
        for (int i = 0; i < numWhiskey; i++) {
            int posicao;
            do {
                posicao = aleatorio.nextInt(50); // Gera uma posicao aleatoria entre 0 e 49
            } while (posicaoNaoEstaLivre(posicao)); 

            posicoesWhiskey.add(posicao);  // Adiciona a posicao ao vetor de posicoes
            posicoesWhiskeyIniciais.add(posicao);    // Salva a posicao para usar no reiniciar jogo
            
            // So atualiza o icone se modo new game
            if (visibilidade) {
                botoes[posicao].setIcon(whiskeyIcon);  // Define a imagem do whiskey no botao da posicao atual
            }   
        }
    }

    private void distribuirArmadilhasPesadas(int numArmadilhas) {
        for (int i = 0; i < numArmadilhas; i++) {
            int posicao;
            do {
                posicao = aleatorio.nextInt(50); // Gera uma posicao aleatoria entre 0 e 49
            } while (posicaoNaoEstaLivre(posicao)); 

            posicoesArmadilhasPesadas.add(posicao);  // Adiciona a posicao ao vetor de posicoes
            posicoesArmadilhasPesadasIniciais.add(posicao);    // Salva a posicao para usar no reiniciar jogo

            // So atualiza o icone se modo new game
            if (visibilidade) {
                botoes[posicao].setIcon(armadilhaPesadaIcon);  // Define a imagem da armadilha no botao da posicao atual
            } 
        }
    }

    private void distribuirArmadilhasLeves(int numArmadilhas) {
        for (int i = 0; i < numArmadilhas; i++) {
            int posicao;
            do {
                posicao = aleatorio.nextInt(50); // Gera uma posicao aleatoria entre 0 e 49
            } while (posicaoNaoEstaLivre(posicao)); 

            posicoesArmadilhasLeves.add(posicao);  // Adiciona a posicao ao vetor de posicoes
            posicoesArmadilhasLevesIniciais.add(posicao);    // Salva a posicao para usar no reiniciar jogo

            // So atualiza o icone se modo new game
            if (visibilidade) {
                botoes[posicao].setIcon(armadilhaLeveIcon); // Define a imagem da armadilha no botao da posicao atual
            }
            
        }
    }

    private void distribuirIndios(int numInimigos) {
        for (int i = 0; i < numInimigos; i++) {
            int posicao;
            do {
                posicao = aleatorio.nextInt(50); // Gera uma posicao aleatoria entre 0 e 49
            } while (posicaoNaoEstaLivre(posicao)); 

            Inimigo inimigo = new Indio("Indio " + (i + 1), 20, 5, 7); // Instancia os Indios
            vetorInimigos.add(inimigo);     // Adiciona o inimigo ao vetor de inimigos
            posicoesInimigos.add(posicao);  // Adiciona a posicao ao vetor de posicoes
            posicoesInimigosIniciais.add(posicao);    // Salva a posicao para usar no reiniciar jogo
            vetorInimigosIniciais.add(inimigo);   // Salva o inimigo para usar no reiniciar jogo
            
            // So atualiza o icone se modo new game
            if (visibilidade) {
                botoes[posicao].setIcon(indioIcon); // Define a imagem do inimigo no botao da posicao atual
            }
            
        }
    }

    private void distribuirRogues(int numInimigos) {
        for (int i = 0; i < numInimigos; i++) {
            int posicao;
            do {
                posicao = aleatorio.nextInt(50); // Gera uma posicao aleatoria entre 0 e 49
            } while (posicaoNaoEstaLivre(posicao)); 

            Inimigo inimigo = new Rogue("Rogue " + (i + 1), 15, 12, 5); // Instancia os rogues
            vetorInimigos.add(inimigo);     // Adiciona o inimigo ao vetor de inimigos
            posicoesInimigos.add(posicao);  // Adiciona a posicao ao vetor de posicoes
            posicoesInimigosIniciais.add(posicao);    // Salva a posicao para usar no reiniciar jogo
            vetorInimigosIniciais.add(inimigo);   // Salva o inimigo para usar no reiniciar jogo 

            if (visibilidade) {
                botoes[posicao].setIcon(rogueIcon); // Define a imagem do inimigo no botão da posicao atual
            }
            
        }
    }

    @Override // Funcao para movimentar o heroi e o comeco das interacoes
    public void keyPressed(KeyEvent e) {
        int keyCode = e.getKeyCode();

        botoes[posicaoHeroi].setIcon(null); // Remove a imagem do heroi do botao anterior

        // Os ifs garantem que o heroi nao vai sair para fora do campoBatalha
        switch (keyCode) {
            case KeyEvent.VK_UP:
                if (posicaoHeroi >= 10) {
                    posicaoAnteriorHeroi = posicaoHeroi;
                    posicaoHeroi -= 10;
                }
                break;
            case KeyEvent.VK_DOWN:
                if (posicaoHeroi < 40) {
                    posicaoAnteriorHeroi = posicaoHeroi;
                    posicaoHeroi += 10;
                }
                break;
            case KeyEvent.VK_LEFT:
                if (posicaoHeroi % 10 != 0) {
                    posicaoAnteriorHeroi = posicaoHeroi;
                    posicaoHeroi -= 1;
                }
                break;
            case KeyEvent.VK_RIGHT:
                if (posicaoHeroi % 10 != 9) {
                    posicaoAnteriorHeroi = posicaoHeroi;
                    posicaoHeroi += 1;
                } 
                break;
        }

        // Interagi de acordo com o que o heroi entrou em contato
        if (posicoesInimigos.contains(posicaoHeroi)) {           
            combateInimigoBasico();

        }else if (posicaoChefao == posicaoHeroi) {
            combateChefao();
        }
        else if (posicoesArmadilhasPesadas.contains(posicaoHeroi)) {
            danoArmadilhaPesada();
        } 
        else if (posicoesArmadilhasLeves.contains((posicaoHeroi))) {
            danoArmadilhaLeve();
        }
        else if (posicoesWhiskey.contains((posicaoHeroi))) {
            adicionarWhiskey();
        }
        else {
            botoes[posicaoHeroi].setIcon(heroiIcon); // Caso contrario so atualiza a posicao do heroi com a imagem
        }

        battlefield.requestFocusInWindow(); // Atualiza o foco para o teclado, assim pode usar setas novamente apos clicar em um botao

    }

    @Override
    public void keyReleased(KeyEvent e) {
        // Nao utilizado
    }

    @Override
    public void keyTyped(KeyEvent e) {
        // Nao utilizado
    }

    // Combate com inimigo basico
    private void combateInimigoBasico() {

        int indiceInimigoAtual = posicoesInimigos.indexOf(posicaoHeroi);  // Pega o indice do inimigo atual na lista
        Inimigo inimigoAtual = vetorInimigos.get(indiceInimigoAtual); // Pega o mesmo inimigo que o heroi encontrou

        JOptionPane.showMessageDialog(this,"        " + inimigoAtual.getNome() + " te emboscou!");
        JanelaCombate janelaCombate = new JanelaCombate(heroi, inimigoAtual); // Abre a nova janela de combate

        // So executa apos a janela de combate for fechada
        janelaCombate.addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosed(WindowEvent e) {
        
                // Caso heroi tenha morrido durante a batalha, fecha a janela
                if (heroi.getHp() <= 0) {
                    dispose();
                }
                // Atualizas as posicoes e icones se o heroi venceu a batalha
                else if (janelaCombate.heroiFugiu() == false) {
                    posicoesInimigos.remove(indiceInimigoAtual);
                    vetorInimigos.remove(indiceInimigoAtual);
                    botoes[posicaoHeroi].setIcon(heroiIcon);
                    updater();
                }
                // Caso ele tenha fugido, nao atualiza e o heroi volta para posicao anterior
                else if (janelaCombate.heroiFugiu() == true){
                    botoes[posicaoAnteriorHeroi].setIcon(heroiIcon);
                    posicaoHeroi = posicaoAnteriorHeroi;
                    updater();
                }
            }
        });
    }

    // Combate com chefao
    private void combateChefao() {
        JOptionPane.showMessageDialog(this, "<VOCE ENCONTROU O CHEFAO> \n<PREPARE-SE PARA BATALHA>");
        Inimigo chefao = new Chefao("Billy The Kid", 50, 20, 10); // Instancia o chefao
        JanelaCombate janelaCombate = new JanelaCombate(heroi, chefao); // Abre a nova janela de combate

        // So executa apos a janela de combate for fechada
        janelaCombate.addWindowListener(new WindowAdapter() {
            @Override // Inicia o jogo de novo
            public void windowClosed(WindowEvent e) {
                dispose();
            }
        });        
    }

    // -0 ate -5 de hp ao contato
    private void danoArmadilhaPesada() {
        int danoPorArmadilha = aleatorio.nextInt(5);

        if (danoPorArmadilha == 0) {
            JOptionPane.showMessageDialog(this, "Voce pisou em uma armadilha de urso, porem\ncom muito cuidado conseguiu desarma-la.\n\n                     Tome cuidado!"); 
        } else {
            heroi.setHp(heroi.getHp() - danoPorArmadilha);
            JOptionPane.showMessageDialog(this, "Voce pisou em uma armadilha de \nurso, perdendo " + danoPorArmadilha + " pontos de vida\n\n        Olha por onde anda!");
        }

        posicoesArmadilhasPesadas.remove(Integer.valueOf(posicaoHeroi)); // Remove a armdilha do vetor
        botoes[posicaoHeroi].setIcon(heroiIcon); // Atualiza o icone do heroi
        updater();
    }

    // -1 de hp ao contato    
    private void danoArmadilhaLeve() {
        heroi.setHp(heroi.getHp() - 1);
        JOptionPane.showMessageDialog(this, "Voce bebeu tanto Whisky que acabou batendo\nem um cacto, perdendo 1 ponto de vida.\n\n         Ta na hora de parar de beber!");

        posicoesArmadilhasLeves.remove(Integer.valueOf(posicaoHeroi)); // Remove a armdilha do vetor
        botoes[posicaoHeroi].setIcon(heroiIcon); // Atualiza o icone do heroi
        updater();
    }

    private void adicionarWhiskey() {
        JOptionPane.showMessageDialog(this, "Voce encontrou um Whiskey\n     Beba com moderacao");
        heroi.setNumWhiskey(heroi.getNumWhiskey() + 1);

        posicoesWhiskey.remove(Integer.valueOf(posicaoHeroi)); // Remove o Whiskey do vetor
        botoes[posicaoHeroi].setIcon(heroiIcon); // Atualiza o icone do heroi
        updater();
    }

    //img escalador generico
    private ImageIcon scaleImageIcon(ImageIcon icon, int x, int y) {
        Image img = icon.getImage();
        Image scaledImg = img.getScaledInstance(x, y, Image.SCALE_SMOOTH);
        return new ImageIcon(scaledImg);
    }

    //img escalador heroi
    private ImageIcon scaleImageIconHero(Hero chara, int x, int y) {
        ImageIcon imgbuf = new ImageIcon(chara.getPortrait().getImage());
        Image img = imgbuf.getImage();
        Image scaledImg = img.getScaledInstance(x, y, Image.SCALE_SMOOTH);
        return new ImageIcon(scaledImg);
    }

    private void updater() {
        infohp.setText("HP: " + heroi.getHp());
        infoatk.setText("ATK: " + heroi.getAtk());
        infodef.setText("DEF: " + heroi.getDef());
        inventinfo.setText("X: " + heroi.getNumWhiskey());
    }

    private void mudarVisibilidade(boolean visibilidade) {
        for (int i = 0; i < 50; i++) {
            if (visibilidade) {
                // Define os icones de acordo com o tipo de objeto presente na posicao
                if (posicoesArmadilhasPesadas.contains(i)) {
                    botoes[i].setIcon(armadilhaPesadaIcon);
                } 
                else if (posicoesArmadilhasLeves.contains(i)) {
                    botoes[i].setIcon(armadilhaLeveIcon);
                } 
                else if (posicoesWhiskey.contains(i)) {
                    botoes[i].setIcon(whiskeyIcon);
                } 
                else if (posicoesInimigos.contains(i)) {
                    int indiceInimigoAtual = posicoesInimigos.indexOf(i);  // Pega o indice do inimigo atual na lista
                    Inimigo inimigoAtual = vetorInimigos.get(indiceInimigoAtual); // Pega o mesmo inimigo
                    if (inimigoAtual instanceof Indio){   // Atualiza o icone de acordo com o inimigo correto
                        botoes[i].setIcon(indioIcon); 
                    } else {
                        botoes[i].setIcon(rogueIcon); 
                    }
                } 
                else if (i == posicaoChefao) {
                    botoes[i].setIcon(billyIcon);
                } 
                else if (i == posicaoHeroi) {
                    botoes[i].setIcon(heroiIcon);
                } 
                else {
                    botoes[i].setIcon(null); // Nenhum icone
                }

              // Ou nao deixa nada visivel alem do heroi e chefao
            } else {
                if (i == posicaoHeroi) {
                    botoes[i].setIcon(heroiIcon);
                }
                else if (i == posicaoChefao) {
                    botoes[i].setIcon(billyIcon);
                } else {
                    botoes[i].setIcon(null); // Esconde o icone
                }
            }
        }
    }

    private void reiniciarJogo() {

        // Limpa todos os icones dos botoes
        for (int i = 0; i < 50; i++) {
            botoes[i].setIcon(null);
        }

        // Limpa todas as listas de posicoes
        posicoesWhiskey.clear();
        posicoesArmadilhasLeves.clear();
        posicoesArmadilhasPesadas.clear();
        posicoesInimigos.clear();
        vetorInimigos.clear();

        // Passa os dados de volta para o vetor de sempre
        posicoesWhiskey.addAll(posicoesWhiskeyIniciais);
        posicoesArmadilhasLeves.addAll(posicoesArmadilhasLevesIniciais);
        posicoesArmadilhasPesadas.addAll(posicoesArmadilhasPesadasIniciais);
        posicoesInimigos.addAll(posicoesInimigosIniciais);
        vetorInimigos.addAll(vetorInimigosIniciais);

        // Restaura as posicoes iniciais do heroi e chefao
        posicaoHeroi = posicaoInicialHeroi;
        posicaoChefao = posicaoInicialChefao;
        botoes[posicaoHeroi].setIcon(heroiIcon);
        botoes[posicaoChefao].setIcon(billyIcon);
        

        // Reseta tudo 
        // Reseta whiskeys
        for (int i = 0; i < posicoesWhiskey.size(); i++) {
            botoes[posicoesWhiskey.get(i)].setIcon(whiskeyIcon);
        }

        // Reseta armadilhas leves
        for (int i = 0; i < posicoesArmadilhasLeves.size(); i++) {
            botoes[posicoesArmadilhasLeves.get(i)].setIcon(armadilhaLeveIcon);
        }

        // Reseta armadilhas pesadas 
        for (int i = 0; i < posicoesArmadilhasPesadas.size(); i++) {
            botoes[posicoesArmadilhasPesadas.get(i)].setIcon(armadilhaPesadaIcon);
        }
        
        // Reseta inimigos 
        for (int i = 0; i < posicoesInimigos.size(); i++) {
            
            int posicao = posicoesInimigos.get(i);

            if (i < 3) {
                botoes[posicao].setIcon(indioIcon); // Primeiro 3 sempre sao Indios

            } else if (i >= 3 && i <= 5) {
                botoes[posicao].setIcon(rogueIcon); // Restantes sempre sao Rogues
            }
        }

        // Mantem visivel ou nao dependendo do modo atual do jogo
        if (!visibilidade) {
            mudarVisibilidade(false);
        }

    
        // Reverte os status do heroi
        heroi.setHp(hpAntesBatalhas); 
        heroi.setAtk(atkAntesBatalhas);  
        heroi.setDef(defAntesBatalhas); 
        heroi.setNumWhiskey(0);
        limiteUsosDica = 3;
        updater();
    }    

    private void verificarImagem(ImageIcon imagemAtual) throws IOException  {
        if (imagemAtual.getImageLoadStatus() != MediaTracker.COMPLETE) {
            throw new IOException("Imagem nao pode ser carregada corretamente");
        }
    }
}
```

## Gunslinger.java
```java
import javax.swing.*;

class Gunslinger extends Hero {

    ImageIcon portrait = new ImageIcon("imgs/Gunslinger.png");


    Gunslinger(String nome, int hp, int atk, int def, int numWhiskey){
        super(nome, hp, atk, def, numWhiskey);

        setbaseHp(17);
        setbaseAtk(7);
        setbaseDef(3);
    }


    // Aumenta em 50% o proximo ataque
    @Override
    public int useSkill() {
        JOptionPane.showMessageDialog(null, "       Voce usou sua Habilidade Especial!\n            Um agil mestre dos revolveres\n\nSeu proximo ataque causa 50% a mais de dano");
        return (this.getAtk() + this.getAtk()*(1/2));
    }

    public ImageIcon getPortrait() {
        return portrait;
    }
}
```


## Hero.java
```java
import javax.swing.*;

abstract class Hero {
    private String nome;
    private int hp;
    private int atk;
    private int def;
    private int numWhiskey;
    private ImageIcon portrait;

    private int basehp;
    private int baseatk;
    private int basedef;

    public Hero(String nome, int hp, int atk, int def, int numWhiskey) {
        this.nome = nome;
        this.hp = hp;
        this.atk = atk;
        this.def = def;
        this.numWhiskey = numWhiskey;

        this.basehp = hp;
        this.baseatk = atk;
        this.basedef = def;
    }

    // getter setter
    public String getNome() {
        return nome;
    }

    public void setNome(String nome) {
        this.nome = nome;
    }

    public int getHp() {
        return hp;
    }

    public void setHp(int hp) {
        this.hp = hp;
    }

    public int getAtk() {
        return atk;
    }

    public void setAtk(int atk) {
        this.atk = atk;
    }

    public int getDef() {
        return def;
    }

    public void setDef(int def) {
        this.def = def;
    }

    public int getNumWhiskey() {
        return numWhiskey;
    }

    public void setNumWhiskey(int numWhiskey) {
        this.numWhiskey = numWhiskey;
    }

    public int getbaseHp() {
        return basehp;
    }

    public int getbaseAtk() {
        return baseatk;
    }

    public int getbaseDef() {
        return basedef;
    }

    public void setbaseHp(int basehp) {
        this.basehp = basehp;
    }

    public void setbaseAtk(int baseatk) {
        this.baseatk = baseatk;
    }

    public void setbaseDef(int basedef) {
        this.basedef = basedef;
    }

    // skill
    public abstract int useSkill();

    public ImageIcon getPortrait() {
        return portrait;
    }
}
```

## Hscreen.java
```java
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;
import javax.swing.border.EmptyBorder;

class Hscreen extends JFrame implements ActionListener {

    // botões
    private JButton Bgunslinger;
    private JButton Boutlaw;
    private JButton Bsheriff;

    private boolean escolhaModoJogo;

    private JLabel lblgunslinger,lbloutlaw,lblsheriff;

    // icones
    ImageIcon gunslingerIcon;
    ImageIcon outlawIcon;
    ImageIcon sheriffIcon;

    public Hscreen(boolean escolhaModoJogo) {
        super("Seleção de Herói");
        this.escolhaModoJogo = escolhaModoJogo;

        // icone da janale
        ImageIcon icon = new ImageIcon("imgs\\WWC2icon.png");
        setIconImage(icon.getImage());

        Container tela = getContentPane();
        setSize(800, 480);
        setLayout(new BorderLayout());
        setLocationRelativeTo(null);

        // tamanho do botão
        Dimension buttonSize = new Dimension(148, 202);

        // escalar as imagens
        gunslingerIcon = scaleImageIcon(new ImageIcon("imgs\\gunslingerbaner.png"), buttonSize.width,
                buttonSize.height);
        outlawIcon = scaleImageIcon(new ImageIcon("imgs\\outlawbaner.png"), buttonSize.width, buttonSize.height);
        sheriffIcon = scaleImageIcon(new ImageIcon("imgs\\sheriffbaner.png"), buttonSize.width, buttonSize.height);

        // botões ja re-escalados
        Bgunslinger = new JButton(gunslingerIcon);
        Boutlaw = new JButton(outlawIcon);
        Bsheriff = new JButton(sheriffIcon);

        // travar tamanho do botão
        Bgunslinger.setPreferredSize(buttonSize);
        Bgunslinger.setMinimumSize(buttonSize);
        Bgunslinger.setMaximumSize(buttonSize);

        Boutlaw.setPreferredSize(buttonSize);
        Boutlaw.setMinimumSize(buttonSize);
        Boutlaw.setMaximumSize(buttonSize);

        Bsheriff.setPreferredSize(buttonSize);
        Bsheriff.setMinimumSize(buttonSize);
        Bsheriff.setMaximumSize(buttonSize);

        // action listeners
        Bgunslinger.addActionListener(this);
        Boutlaw.addActionListener(this);
        Bsheriff.addActionListener(this);

        // imagem de fundo
        Hselect backimg = new Hselect("imgs\\HSelectinfo2.png");

        //info de personagens
        lblgunslinger= new JLabel("Gunslinger");
        lblgunslinger.setForeground(Color.BLACK);
        lblgunslinger.setFont(new Font("Arial", Font.BOLD, 15));
        lbloutlaw= new JLabel("Outlaw");
        lbloutlaw.setForeground(Color.BLACK);
        lbloutlaw.setFont(new Font("Arial", Font.BOLD, 15));
        lblsheriff= new JLabel("Sheriff");
        lblsheriff.setForeground(Color.BLACK);
        lblsheriff.setFont(new Font("Arial", Font.BOLD, 15));

        JPanel infopanel= new JPanel (new FlowLayout(FlowLayout.CENTER, 10,10));
        infopanel.setOpaque(false);
        infopanel.add(lblgunslinger);
        infopanel.add(Box.createHorizontalStrut(70));
        infopanel.add(lbloutlaw);
        infopanel.add(Box.createHorizontalStrut(80));
        infopanel.add(lblsheriff);
        infopanel.setBounds(190,10,400,400);
        infopanel.setForeground(Color.BLACK);


        // painel de botões
        JPanel buttonPanel = new JPanel(new FlowLayout(FlowLayout.CENTER, 10, 10));
        buttonPanel.setOpaque(false); // fazer botão transparente
        buttonPanel.setBorder(new EmptyBorder(40, 0, 0, 0)); // espaço para baixo
        buttonPanel.add(Bgunslinger);
        buttonPanel.add(Boutlaw);
        buttonPanel.add(Bsheriff);
        buttonPanel.setBounds(100, 20, 600, 400);

        // labels
        JLabel Lgunslinger = new JLabel(
                "<html>Gunslinger: Um agil mestre em revolvers <br> <strong>Skill:<strong> Trick Shot (Próximo ataque ira dar 50%+ dano)</html>");
        Lgunslinger.setForeground(Color.BLACK);
        Lgunslinger.setFont(new Font("Arial", Font.BOLD, 12));
        JLabel Loutlaw = new JLabel(
                "<html>Outlaw: Um foragido mortifero, especialista em escapar da lei <br> <strong>Skill:<strong> Super Foco (Esquiva do próximo ataque)</html>");
        Loutlaw.setForeground(Color.BLACK);
        Loutlaw.setFont(new Font("Arial", Font.BOLD, 12));
        JLabel Lsheriff = new JLabel(
                "<html>Sheriff: A lei em pessoa, não são muitos que conseguem escapar sua perseguição sem fim <br> <strong> Skill:<strong> Prova de Justiça (Recebe metade do dano no próximo ataque)</html>");
        Lsheriff.setForeground(Color.BLACK);
        Lsheriff.setFont(new Font("Arial", Font.BOLD, 12));

        JPanel labelPanel = new JPanel();
        labelPanel.setLayout(new BoxLayout(labelPanel, BoxLayout.Y_AXIS));
        labelPanel.setOpaque(false);
        labelPanel.setBorder(new EmptyBorder(60, 180, 0, 0));// Espaço para baixo e direita
        labelPanel.add(Lgunslinger);
        labelPanel.add(Box.createRigidArea(new Dimension(0, 10))); // espaço entre as labels
        labelPanel.add(Loutlaw);
        labelPanel.add(Box.createRigidArea(new Dimension(0, 10))); // espaço entre as labels
        labelPanel.add(Lsheriff);
        labelPanel.setBounds(0,250,800,400);


        backimg.setLayout(null);
        backimg.add(buttonPanel, BorderLayout.NORTH);
        backimg.add(labelPanel, BorderLayout.CENTER);
        backimg.add(infopanel);

        // adicionando info
        tela.add(backimg, BorderLayout.CENTER);

        setVisible(true);
    }

    @Override
    public void actionPerformed(ActionEvent action) {
        if (action.getSource() == Bgunslinger) {

            Gunslinger gunslinger = new Gunslinger("Gunslinger", 17, 7, 3, 0);
            ChScreen chScreen = new ChScreen(gunslinger, escolhaModoJogo);
            chScreen.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
            dispose();

        }
        if (action.getSource() == Boutlaw) {

            Outlaw outlaw = new Outlaw("Outlaw", 12, 12, 2, 0);
            ChScreen chScreen = new ChScreen(outlaw, escolhaModoJogo);
            chScreen.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
            dispose();

        }
        if (action.getSource() == Bsheriff) {

            Sheriff sheriff = new Sheriff("Sheriff", 21, 7, 6, 0);
            ChScreen chScreen = new ChScreen(sheriff, escolhaModoJogo);
            chScreen.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
            dispose();

        }
    }

    // resizer de imagem
    private ImageIcon scaleImageIcon(ImageIcon icon, int width, int height) {
        Image img = icon.getImage();
        Image scaledImg = img.getScaledInstance(width, height, Image.SCALE_SMOOTH);
        return new ImageIcon(scaledImg);
    }

}
```

## Hselect.java
```java
import java.awt.*;
import javax.swing.*;

class Hselect extends JPanel {
    private Image backgroundImage;


    public Hselect(String imagePath) {
        backgroundImage = new ImageIcon("imgs/HSelectinfo2.png").getImage();
    }

    @Override
    protected void paintComponent(Graphics g) {
        super.paintComponent(g);
        // Imagem de fundo
        g.drawImage(backgroundImage, 0, 0, getWidth(), getHeight(), this);
    }
}
```

## ImagePanel.java

```java
import java.awt.*;
import javax.swing.*;

class ImagePanel extends JPanel {
    private Image image;
    private int x, y;

    public ImagePanel(Image image, int x, int y) {
        this.image = image;
        this.x = x;
        this.y = y;
        setPreferredSize(new Dimension(x, y));
    }

     @Override
        protected void paintComponent(Graphics g) {
            super.paintComponent(g);
            // Imagem de fundo
            g.drawImage(image, 0, 0, getWidth(), getHeight(), this);
        }
}
```

## Indio.java
```java
import javax.swing.ImageIcon;

public class Indio extends Inimigo {

    ImageIcon portrait = new ImageIcon("imgs//Indio.png");

    Indio(String nome, int hp, int atk, int def) {
        super(nome, hp, atk, def);
    }

    public ImageIcon getPortrait() {
        return portrait;
    }
}
```


## Inimigo.java
```java
import javax.swing.ImageIcon;

public abstract class Inimigo {

    private String nome;
    private int hp;
    private int atk;
    private int def;
    private ImageIcon portrait;

    public Inimigo(String nome, int hp, int atk, int def) {
        this.nome = nome;
        this.hp = hp;
        this.atk = atk;
        this.def = def;
    }

    public String getNome() {
        return nome;
    }

    public void setNome(String nome) {
        this.nome = nome;
    }

    public int getHp() {
        return hp;
    }

    public void setHp(int hp) {
        this.hp = hp;
    }

    public int getAtk(){
        return atk;
    }

    public void setAtk(int atk) {
        this.atk = atk;
    }

    public int getDef(){
        return def;
    }

    public void setDef(int def) {
        this.def = def;
    }

    public ImageIcon getPortrait() {
        return portrait;
    }
}
```


## JanelaCombate.java
```java
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.util.Random;
import javax.swing.*;


public class JanelaCombate extends JFrame {
    private Hero heroi;          
    private Inimigo inimigoAtual; 
    private JLabel lblHeroHp, lblHeroAtk, lblHeroDef; // Labels para exibir stats do heroi
    private JLabel lblInimigoHp, lblInimigoAtk, lblInimigoDef; // Labels para exibir stats do inimigo
    private boolean heroiFugiu = false;

    // Variaveis globais
    Random aleatorio = new Random();
    boolean habilidadeEspecialUsada = false;
    boolean habilidadeEspecialAtiva = false;
    int statusModificado;
    int atkTotal = 0;
    int defTotal = 0;
    int diferenca = 0;


    public JanelaCombate(Hero heroi, Inimigo inimigoAtual) {
        this.heroi = heroi;
        this.inimigoAtual = inimigoAtual;

        // Caracteristicas da janela de combate
        setTitle("Combate com " +  inimigoAtual.getNome());   // Titulo 
        setSize(400, 300);                       // Dimensoes
        setLayout(new GridLayout(5, 2));            // Formato

        // Inicializa os labels dos stats do heroi e do inimigo
        lblHeroHp = new JLabel("HP do Heroi: " + heroi.getHp());
        lblHeroAtk = new JLabel("Atk do Heroi: " + heroi.getAtk());
        lblHeroDef = new JLabel("Def do Heroi: " + heroi.getDef());
        lblInimigoHp = new JLabel("HP do Inimigo: " + inimigoAtual.getHp());
        lblInimigoAtk = new JLabel("Atk do Inimigo: " + inimigoAtual.getAtk());
        lblInimigoDef = new JLabel("Def do Inimigo: " + inimigoAtual.getDef());

        // Botao Atacar + ActionListener
        JButton botaoAtacar = new JButton("Atacar");
        botaoAtacar.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                combate(); 
            }
        });

        // Botao Beber Whisky + ActionListener
        JButton botaoWhisky  = new JButton("Beber Whisky");
        botaoWhisky.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {

                if (heroi.getNumWhiskey() == 0 ){
                    JOptionPane.showMessageDialog(null, "Acabou o estoque camarada...");
                }else {
                    heroi.setHp(heroi.getHp() + 20); // Recupera 20 de HP, por exemplo
                    heroi.setNumWhiskey(heroi.getNumWhiskey() - 1);
                    atualizarStatusDaTela(); // Atualiza a interface com o novo valor de HP
                    JOptionPane.showMessageDialog(null, "Voce bebeu whisky e recuperou 20 de vida!");
                }    
            }
        });

        // Botao usarHabilidadeEspecial + ActionListener
        JButton botaoHabilidadeEspecial  = new JButton("Usar Habilidade Especial");
        botaoHabilidadeEspecial.addActionListener(new ActionListener() {
            
            @Override
            public void actionPerformed(ActionEvent e) {

                if (habilidadeEspecialUsada == true){
                    JOptionPane.showMessageDialog(null, "Voce ja usou sua habilidade especial contra esse inimigo");
                } else {
                    statusModificado = heroi.useSkill();
                    habilidadeEspecialUsada = true;
                    habilidadeEspecialAtiva = true;
                }
            }
        });

        // Botao botaoFugir + ActionListener
        JButton botaoFugir  = new JButton("Fugir");
        botaoFugir.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                if (inimigoAtual instanceof Chefao){
                    JOptionPane.showMessageDialog(null, "Ninguem consegue escapar da batalha final!!!");  
                    return;  
                } else if (heroi.getHp() - 3 <= 0) {
                    JOptionPane.showMessageDialog(null, "Voce esta cansado demais para fugir");  
                    return;  
                }

                JOptionPane.showMessageDialog(null, "Voce saiu correndo e acabou tropecando, sofrendo 3 de dano no processo... seu covarde!");
                heroi.setHp(heroi.getHp() - 3);
                heroiFugiu = true;

                dispose(); // Fecha a janela de combate
            }
        });

        // Adiciona os componentes na janela
        add(lblHeroHp);
        add(lblInimigoHp);
        add(lblHeroAtk);      
        add(lblInimigoAtk);
        add(lblHeroDef);
        add(lblInimigoDef);
        add(botaoAtacar);     
        add(botaoWhisky);
        add(botaoHabilidadeEspecial);
        add(botaoFugir);

        // Mais caracteristicas da janela de combate
        setDefaultCloseOperation(JFrame.DISPOSE_ON_CLOSE); // So fecha essa janela e nao toda o jogo
        setLocationRelativeTo(null); // Começa no centro
        setFocusable(true);  // Tira a 'sombra' do botao (tambem deve fazer mais alguma coisa que nao sei)
        setVisible(true);            // Visivel
    }

    // Logica de combate
    private void combate() {

        // Calculos para o combate (heroi atacando) (com habilidade especial) 
        if (habilidadeEspecialAtiva) {
            if (heroi instanceof Gunslinger) {
                atkTotal = heroi.getAtk() + aleatorio.nextInt(10) + statusModificado;
                defTotal = inimigoAtual.getDef() + aleatorio.nextInt(10);
                diferenca = atkTotal - defTotal;

                // Tem 50% a mais de dano
                realizarCombateHeroiAtacando(atkTotal, defTotal, diferenca);
                habilidadeEspecialAtiva = false;
            }

            else if (heroi instanceof Outlaw) {
                // Pula o turno do inimigo
                diferenca = calcularDiferencaHeroi();
                realizarCombateHeroiAtacando(atkTotal, defTotal, diferenca);
                
                JOptionPane.showMessageDialog(this, "Voce desviou do ataque do inimigo");
                habilidadeEspecialAtiva = false;
                
                // Caso inimigo tenha morrido
                if (inimigoAtual.getHp() <= 0) {
                    // Caso a luta tenha sido contra o chefao mostra mensagem de end game (VOLTAR PARA MENU INICIAL)
                    if (inimigoAtual instanceof Chefao) {
                        JOptionPane.showMessageDialog(this, "Parabens!!!");
                        dispose(); // Fecha a janela de combate
                        return;
                    } else {
                        adicionarAtributoAleatorio();
                    }
                }
        
                atualizarStatusDaTela();
                return;
            }

            else if (heroi instanceof Sheriff) {
                // Ataque normal
                diferenca = calcularDiferencaHeroi();                
                realizarCombateHeroiAtacando(atkTotal, defTotal, diferenca);
            }

        } else {
            // Combate (heroi atacando) (sem habilidade especial)
            diferenca = calcularDiferencaHeroi();
            realizarCombateHeroiAtacando(atkTotal, defTotal, diferenca);
        }

        


        // Caso inimigo tenha morrido
        if (inimigoAtual.getHp() <= 0) {
            // Caso a luta tenha sido contra o chefao mostra mensagem de end game (VOLTAR PARA MENU INICIAL)
            if (inimigoAtual instanceof Chefao) {
                JOptionPane.showMessageDialog(this, "O inimigo final cai ao seus pes");
                JOptionPane.showMessageDialog(this, "Parabens pela sua vitoria!!!");
                new Mwindows();
                dispose(); // Fecha a janela de combate
                return;
            } else {
                adicionarAtributoAleatorio();
            }

        } else {
            if (habilidadeEspecialAtiva) {
                if (heroi instanceof Sheriff) {
                    // Recebe metade do dano do inimigo
                    diferenca = calcularDiferencaHeroi();
                    realizarCombateInimigoAtacando(atkTotal, defTotal, diferenca / 2);
                    habilidadeEspecialAtiva = false;
                }

            } else {
                // Combate (inimigo atacando)
                diferenca = calcularDiferencaInimigo();
                realizarCombateInimigoAtacando(atkTotal, defTotal, diferenca);
            }
        }



        
        // Caso o heroi tenha morrido (VOLTAR PARA MENU INICIAL)
        if (heroi.getHp() <= 0) {
            JOptionPane.showMessageDialog(this, "Seu HP chegou em 0, voce perdeu!\n                       :(");
            new Mwindows();
            dispose(); // Fecha a janela de combate
        }

        // Refresh na tela de status
        atualizarStatusDaTela();
    }

    private void realizarCombateHeroiAtacando(int atkTotal, int defTotal, int diferenca) {
        if (defTotal >= atkTotal) {
            JOptionPane.showMessageDialog(this, "O inimigo defendou todo o seu ataque!!!");
        }
        else {
            JOptionPane.showMessageDialog(this, "Voce infligiu " + diferenca + " de dano.");
            inimigoAtual.setHp((inimigoAtual.getHp() - diferenca));  // Atualiza a vida do inimigo
        }
    }

    private void realizarCombateInimigoAtacando(int atkTotal, int defTotal, int diferenca) {
        // Mesma logica de combate de antes mas agora com o heroi recebendo o ataque
        if (defTotal >= atkTotal) {
            JOptionPane.showMessageDialog(this, "Voce defendou completamente o ataque do inimigo!!!");
        }
        else {
            JOptionPane.showMessageDialog(this, "Voce sofreu " + diferenca + " de dano.");
            heroi.setHp((heroi.getHp() - diferenca));  // Atualiza a vida do inimigo
        }
    }

    private int calcularDiferencaHeroi() {
        atkTotal = heroi.getAtk() + aleatorio.nextInt(10);
        defTotal = inimigoAtual.getDef() + aleatorio.nextInt(10);
        return diferenca = atkTotal - defTotal;
    }

    private int calcularDiferencaInimigo() {
        atkTotal = inimigoAtual.getAtk() + aleatorio.nextInt(10);
        defTotal = heroi.getDef() + aleatorio.nextInt(10);
        return diferenca = atkTotal - defTotal;
}

    private void adicionarAtributoAleatorio() {
        int recompensaAleatoria = aleatorio.nextInt(3);           

        //  Concede ao heroi um atributo aleatorio
        switch (recompensaAleatoria) {
            case 0:
                heroi.setHp(heroi.getHp() + 1);
                JOptionPane.showMessageDialog(this, "Voce venceu a batalha e recebeu +1 ponto de Vida");
                break;
            case 1:
                heroi.setAtk(heroi.getAtk() + 1);
                JOptionPane.showMessageDialog(this, "Voce venceu a batalha e recebeu +1 ponto de Ataque");
                break;
            case 2:
                heroi.setDef(heroi.getDef() + 1);
                JOptionPane.showMessageDialog(this, "Voce venceu a batalha e recebeu +1 ponto de Defesa");
                break;
            default:
                System.out.println("Erro dentro do switch!");
                throw new AssertionError();
        }

        dispose(); // Fecha a janela de combate
    }

    public boolean heroiFugiu() {
        return heroiFugiu;
    }

    // Atualiza labels de HP na janela
    private void atualizarStatusDaTela() {
        lblHeroHp.setText("HP do Heroi: " + heroi.getHp());             
        lblInimigoHp.setText("HP do Inimigo: " + inimigoAtual.getHp()); 
    }

}
```

## main.java
```java
public class main {
    public static void main(String[] args) {        
        
        new Mwindows();

        Hero heroi1 = new Gunslinger("Gunslinger", 100, 15, 1, 0);
        Hero heroi2 = new Outlaw("Outlaw", 1000, 1000, 1, 0);
        Hero heroi3 = new Sheriff("Sheriff", 100, 15, 1, 0);
        
        //new Field(heroi2, true);

    }
}
```

## Mwindows.java
```java
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

class Mwindows extends JFrame implements ActionListener {

  private JButton Bstart;
  private JButton Bdebug;
  private JButton Bexit;

  public Mwindows() {
    super("Wild West Crusade");

    // Icone
    ImageIcon icon = new ImageIcon("imgs/WWC2icon.png");
    setIconImage(icon.getImage());

    Container tela = getContentPane();
    setSize(800, 480);
    setLayout(new BorderLayout());
    setLocationRelativeTo(null);

    // botões
    Bstart = new JButton("Novo Jogo");
    Bdebug = new JButton("Debug");
    Bexit = new JButton("Sair");

    // leitores para botões
    Bstart.addActionListener(this);
    Bdebug.addActionListener(this);
    Bexit.addActionListener(this);

    // Imagem de fundo
    backgroundimg backimg = new backgroundimg("imgs/Coverart2.png");

    // painel de botões
    JPanel buttonPanel = new JPanel(new FlowLayout(FlowLayout.CENTER, 10, 10));
    buttonPanel.setOpaque(false); // background dos botões transparente
    buttonPanel.add(Bstart);
    buttonPanel.add(Bdebug);
    buttonPanel.add(Bexit);

    // adicionando os elementos na tela
    backimg.setLayout(new BorderLayout());
    backimg.add(buttonPanel, BorderLayout.SOUTH);

    // adicionando a imagem
    tela.add(backimg, BorderLayout.CENTER);

    setVisible(true);
  }

  public void actionPerformed(ActionEvent action) {
    if (action.getSource() == Bstart) {

      Hscreen Hscreen = new Hscreen(false);
      Hscreen.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
      dispose();

    }
    
    if (action.getSource() == Bdebug) {
      
      Hscreen Hscreen = new Hscreen(true);
      Hscreen.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
      dispose();

    }
    if (action.getSource() == Bexit) {

      JOptionPane.showMessageDialog(this, "Saindo do Jogo", "Info", JOptionPane.INFORMATION_MESSAGE, null);

      System.exit(0);
    }

  }
}
```

## Outlaw.java
```java
import javax.swing.*;

class Outlaw extends Hero {

    ImageIcon portrait = new ImageIcon("imgs/Outlaw.png");


    Outlaw(String nome, int hp, int atk, int def, int numWhiskey){
        super(nome, hp, atk, def, numWhiskey);

        setbaseHp(12);
        setbaseAtk(12);
        setbaseDef(2);
    }

    // skill
    @Override
    public int useSkill() {
        JOptionPane.showMessageDialog(null, "       Voce usou sua Habilidade Especial!\nUm fora da lei mortal, mestre em driblar a lei");
        return 1;
    }

    public ImageIcon getPortrait() {
        return portrait;
    }

}
```

## Rogue.java
```java
import javax.swing.ImageIcon;

public class Rogue extends Inimigo {

    ImageIcon portrait = new ImageIcon("imgs\\Rogue.png");

    Rogue(String nome, int hp, int atk, int def) {
        super(nome, hp, atk, def);
    }

    public ImageIcon getPortrait() {
        return portrait;
    }
}
```

## Sheriff.java
```java
import javax.swing.*;

class Sheriff extends Hero{

    ImageIcon portrait = new ImageIcon("imgs/Sheriff.png");
      
    Sheriff(String nome, int hp, int atk, int def, int numWhiskey){
        super(nome, hp, atk, def, numWhiskey);

        setbaseHp(21);
        setbaseAtk(7);
        setbaseDef(6);
    }

    //skill
    @Override
    public int useSkill() {
        JOptionPane.showMessageDialog(null, "                       Voce usou sua Habilidade Especial!\nA lei encarnada, poucos podem escapar de sua perseguicao sem fim");
        return 1;
    }

    public ImageIcon getPortrait() {
        return portrait;
    }
}
```

## victory.java

```java
import javax.swing.*;

class victory extends JDialog{

  ImageIcon img;
  JButton back, sair;

  public victory(JFrame parent, String title, String path){
    super(parent, title, true);

    img= new ImageIcon(path);
    
    setSize(800, 480);
    setLocationRelativeTo(parent);;
    setLayout(null);

    JLabel ImageLabel= new JLabel(img);
    ImageLabel.setBounds(0, 0, 800, 480);
    add(ImageLabel);

    
  }
}
``` 