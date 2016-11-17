 // TypeScript file



class AstarMy extends egret.Sprite {

    public constructor() {
        super();
        this.creatMap();
        this.creatWall(3, 2);
        this.creatWall(3, 1);
        this.creatWall(3, 3);
        this.creatWall(3, 4);
        this.creatWall(3, 5);
        //创建起点
        this.creatA(0, 4);
        this.creatA(5, 5);
        // console.log(this.wall[1].y,this.wall[1]["y"],this.isWall(3,0));
        this.findPath(this.hero);

    }

    private cow = 8;
    private col = 8;

    private openPath = [];
    private closePath = [];

    private wall = [{ x: 3, y: 2 },
        { x: 3, y: 1 },
        { x: 3, y: 3 },
        { x: 3, y: 4 },
        { x: 3, y: 5 },
    ];

    private hero = {
        x: 0,
        y: 4
    }

    private goodNode = {
        x: 0,
        y: 0

    }

    private amy = {
        x: 5,
        y: 5
    }

    private creatMap() {
        for (var i = 0; i < this.cow; i++) {
            for (var j = 0; j < this.col; j++) {
                var shp: egret.Shape = new egret.Shape();
                shp.x = 50 * i;
                shp.y = 50 * j;
                shp.graphics.lineStyle(1, 0x000000);
                shp.graphics.beginFill(0xffffff, 1);
                shp.graphics.drawRect(0, 0, 50, 50);
                shp.graphics.endFill();
                this.addChild(shp);
            }
        }
    }
    private creatWall(x, y) {
        let shp: egret.Shape = new egret.Shape();
        shp.x = 50 * x;
        shp.y = 50 * y;
        shp.graphics.lineStyle(1, 0x000000);
        shp.graphics.beginFill(0x005e8f, 1);
        shp.graphics.drawRect(0, 0, 50, 50);
        shp.graphics.endFill();
        this.addChild(shp);
    }

    //创建起点
    private creatA(x, y) {
        let shp: egret.Shape = new egret.Shape();
        shp.x = 50 * x
        shp.y = 50 * y
        shp.graphics.beginFill(0xff0000, 1);
        shp.graphics.drawRect(0, 0, 50, 50);
        shp.graphics.endFill();
        this.addChild(shp);

    }
    //创建路径
    private creatPathShp(x, y) {
        let shp: egret.Shape = new egret.Shape();
        shp.x = 50 * x
        shp.y = 50 * y
        shp.graphics.beginFill(0xCC6EC4, 1);
        shp.graphics.drawRect(0, 0, 50, 50);
        shp.graphics.endFill();
        this.addChild(shp);

    }


    private findPath(hero: any) {
        if (hero == this.amy) {
            console.log("到目的地了")
            return;
        } else {
            this.findNextHero(hero);
        }
    }
    //p判断该点是否是墙壁 并且放入开放列表
    private pushOpenList(x, y) {
        if (this.isWall(x, y) && this.isHaveOpen(x, y)) {
            this.openPath.push({ 'x': x, 'y': y })
        } else {
            return null;
        }
    }


    private isHaveOpen(x, y) {
        if (this.openPath.length > 0) {
            for (let i = 0; i < this.openPath.length; i++) {
                if (this.openPath[i].x == x && this.openPath[i].y == y) {
                    return false;
                }
            }

            return true;
        }

        return true;
    }


    private findNextHero(hero: any) {
        let xx: boolean = hero.x;
        let yy: boolean = hero.y;

        let x1: boolean = hero.x - 1 >= 0;
        let y1: boolean = hero.y - 1 >= 0;

        let x2: boolean = hero.x + 1 < this.cow;
        let y2: boolean = hero.y + 1 < this.col;
        // 左
        (x1 && y1) ? this.pushOpenList(x1, y1) : null;
        (x1 && yy) ? this.pushOpenList(x1, yy) : null;
        (x1 && y2) ? this.pushOpenList(x1, y2) : null;
        // 上
        (xx && y1) ? this.pushOpenList(xx, y1) : null;
        // 下
        (xx && y2) ? this.pushOpenList(xx, y2) : null;
        // 右
        (x2 && y1) ? this.pushOpenList(x1, y1) : null;
        (x2 && yy) ? this.pushOpenList(x1, yy) : null;
        (x2 && y2) ? this.pushOpenList(x1, y2) : null;

        if (this.openPath.length > 0) {
            let tmp = this.sqrtMath(this.hero, this.openPath[0], this.amy);
            let tmpNum = 0;
            for (let i = 0; i < this.openPath.length; i++) {
                if (tmp < this.sqrtMath(this.hero, this.openPath[i], this.amy)) {
                    tmp = this.sqrtMath(this.hero, this.openPath[i], this.amy)
                    tmpNum = i;
                }
            }

            this.goodNode.x = this.openPath[tmpNum].x;
            this.goodNode.y = this.openPath[tmpNum].y;
            this.creatPathShp(this.goodNode.x, this.goodNode.y)
            this.findPath(this.goodNode);

        }

    }



    //  计算2点之间的距离 f=g+h;
    private sqrtMath(hero: any, node: any, amy: any) {
        let dx = hero.x - node.x;
        let dy = hero.y - node.y;
        let hx = amy.x - node.x;
        let hy = amy.y - node.y;
        return Math.sqrt(dx * dx + dy * dy) + Math.sqrt(hx * hx + hy * hy);
    }

    // 判断是否是墙壁
    private isWall(x, y) {
        for (let i = 0; i < this.wall.length; i++) {
            if (this.wall[i].x == x && this.wall[i].y == y) {
                return false;
            }
        }
        return true;
    }
}
