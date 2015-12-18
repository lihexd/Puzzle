# Tizen-App-Puzzle

## 概述

Puzzle是一款流行的益智游戏。这款游戏的玩法很简单，游戏初始时会将一张图片打分割成16个小方块并打乱，游戏玩家每次可以选择上下左右滑动，每滑动一次，就能改变其中一小块的位置，玩家需要将图片还原即可完成游戏。

## 算法介绍

Puzzle基于TIZEN web project开发，主要使用了Html，CSS与Javascript技术。通过在ontouchstart、ontouchmove和ontouchend方法中计算手指触碰位移来判断手指滑动方向，从而进行上下左右滑动等操作。


```js
function gamepuzzle(container)  
{  
	this.container = container;  
	this.tiles = new Array(16);  
}  
var j;
gamepuzzle.prototype = {    
		init: function(){    
			var i, len, tile;    
			for(i = 0, len = this.tiles.length; i < len; i++){    
				tile = this.newTile((i*7)%16);    
				tile.setAttribute('index', i);    
				this.container.appendChild(tile);    
				this.tiles[i] = tile;    
			}    
		},    
		newTile: function(val){  
			var tile = document.createElement('div');  
			this.setTileVal(tile, val);  
			return tile;  
		},  
		setTileVal: function(tile, val){  
			tile.className = 'tile tile' + val;  
			tile.setAttribute('val', val);  
		},  
		move:function(direction){//move  
			switch(direction){  
			case 1://down  
				if(j >= 4){  
					this.change(this.tiles[j - 4], this.tiles[j]);  
					j -= 4;  
				}  
				break;  
			case 0://up  
				if(j <= 11){  
					this.change(this.tiles[j + 4], this.tiles[j]);  
					j += 4;  
				}  
				break;  
			case 3://right  
				if(j % 4 !== 0){  
					this.change(this.tiles[j - 1], this.tiles[j]);  
					j -= 1;  
				}  
				break;  
			case 2://left  
				if(j % 4 !== 3){  
					this.change(this.tiles[j + 1], this.tiles[j]);  
					j += 1;  
				}  
				break;  
			}  
			this.end();  

		},  
		change: function(prevTile, currTile){
			var prevVal = prevTile.getAttribute('val'),
			currVal = currTile.getAttribute('val');
			this.setTileVal(prevTile, currVal);
			this.setTileVal(currTile, prevVal);
		},
		end: function(){
			var i,len;
			for(i = 0, len = this.tiles.length; i < len; i++){
				if(this.tiles[i].getAttribute('val') == i)
					continue;
				else break;
			}
			if(i == len)
			{
				stopCount();
				alert('Congratulation!Press OK to select picture again.');
				window.location = "changepic.html";
			}
		},
		clean: function(){
			var i, len;
			for(i = 0, len = this.tiles.length; i < len; i++){
				this.container.removeChild(this.tiles[i]);
			}
			this.tiles = new Array(16);
		}

}
```
