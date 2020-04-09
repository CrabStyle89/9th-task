public class Solution {
   public int OrangesRotting(int[][] grid) {
        if(grid.Length==0) return 0;                //checking grid for any Oranges
        int minutes=0,fresh=0;
        Queue<int[]> rotten=new Queue<int[]>();     //create queue for rotten oranges
        for(int i=0;i<grid.Length;i++){
            for(int j=0;j<grid[0].Length;j++){
                if(grid[i][j]==2){                  //if grid has any rotten oranges we added them to queue
                    rotten.Enqueue(new int[]{i,j});
                }
                else if(grid[i][j]==1) fresh++;      //if orange is fresh we increment our counter
            }
        }
        if(fresh==0)return 0;                        // checking for any fresh in grid 
        List<int[]> dirs=new List<int[]>{            //List of coordinates for checking neighbors coordinates 
            new int[]{1,0},
            new int[]{-1,0},
            new int[]{0,1},
            new int[]{0,-1}
        };
        while(rotten.Any()){                         //if queue is not empty we checking neigbors for fres or rotten oranges   
            minutes++;                               //or for emty cels
            int count=rotten.Count;
            for(int i=0;i<count;i++){
                int[] point=rotten.Dequeue();         //get coordinates of rotten one
                foreach(int[] dir in dirs){
                    int x=point[0]+dir[0];            //checking neighbors
                    int y=point[1]+dir[1];
                    if(x<0||y<0||x==grid.Length||y==grid[0].Length||grid[x][y]==2||grid[x][y]==0) continue;
                    grid[x][y]=2;                     //if condition false we get one more rotten orange    
                    rotten.Enqueue(new int[]{x,y});   //get him in queue
                    fresh--;                          
                }
            }
            
        }
        if(fresh>0)return -1;
        else return minutes-1;
    }
}
